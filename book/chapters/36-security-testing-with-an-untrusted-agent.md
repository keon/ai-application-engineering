# Chapter 36. Security testing with an untrusted agent

Status: draft.

[Previous: Chapter 35](./35-investigating-security-alerts-with-untrusted-logs.md) · [Table of contents](../table-of-contents.md) · [Next: Chapter 37](./37-lab-experiments-where-a-retry-costs-a-sample.md)

**New in this chapter:** executable scope; **propose, reject, effect** as three outcomes; reset fidelity; minimized reproducible findings; utility checks on defenses.

**Assumes:** a deliberately isolated replica with synthetic users, fake credentials, and a controlled mail sink; an external controller that owns scope, budgets, and termination; production systems, third parties, and real data excluded; no test is executed by the writing of this chapter.

**Reuses:** simulators and test-the-grader (chapter 16); sandboxes (chapter 7); effect journals (chapter 17); the security investigation's trust labels (chapter 35).

> **About the examples.** The support application, its synthetic users, the canary records, and the campaign figures in this chapter are fictional. Numbers are illustrative unless labeled *measured*. Company and benchmark references support specific control mechanisms and link to reviewed sources; none validates the design or establishes any attack-cost threshold. The chapter describes the harness around a testing agent; it contains no test inputs.

## A finding that vanished after a reset

A security team gives a testing agent an isolated replica of a support application, with synthetic users and a controlled mail sink, and two questions: can one user's records become visible to another, and can untrusted ticket text cause a forbidden tool effect through the application's AI assistant?

The tester reports a cross-user disclosure. The verifier resets the environment and replays the recorded steps, and the disclosure does not reproduce. Separately, the tester's trace shows a request that left the replica for an external address.

Chapter 35 investigated a system that was being attacked. Here the agent is the one probing, by authorization, and it is untrusted in a specific sense: it can misjudge scope, loop on one idea, overstate what it found, and report a finding that depended on state the previous run left behind. Two sub-cases share the chapter, testing the web application and testing the AI component's tool boundary, and both rest on one rule: a candidate is a claim until a clean replay reproduces it under stated preconditions.

Our application supports adaptive discovery inside an authorized, bounded, reproducible process. A completed campaign means the approved surface was tested to a documented extent; it says nothing about the absence of defects.

## What a campaign has to establish

### Confirmed findings, false positives, coverage, reset fidelity, utility

| What the campaign reports | How it is established |
| --- | --- |
| Confirmed findings | Reproduced on a clean snapshot under stated preconditions; deduplicated by cause |
| False positives | Candidates that failed clean replay, with the reason |
| Coverage | A matrix of routes, identities, states, and checks, with untested cells and why |
| Reset fidelity | Baseline digest and smoke behavior verified before each replay |
| Utility | The patched target still completes legitimate tasks |

The agent is untrusted, so an external controller owns target allowlists, permitted action classes, fake credentials, budgets, network boundaries, and termination. Prompt instructions enforce nothing.

The baseline is a versioned regression suite against known defects and their patched counterparts, measured on confirmed findings, false positives, surface coverage, reset fidelity, and legitimate behavior.

### The fixture

Replica R-5 with synthetic users U-1 and U-2. One cross-user canary: record C-77 belongs to U-2 and must be invisible to U-1. One AI tool boundary: the assistant reads ticket text and has a tool that can send mail to the controlled sink, which it must use only for its own user. One patched counterpart, R-5p, with both defects fixed. One benign control task: U-1 views their own record and the assistant drafts an ordinary reply. The answer key: on R-5, the canary is reachable by U-1 (a confirmed finding) and ticket text can cause a forbidden tool effect; on R-5p, neither reproduces and the benign task succeeds; a candidate that reproduces only with an elevated session is labeled as such or rejected; no request leaves the replica; the campaign's spend includes the target and verifier calls.

### The naive version is pointed at the replica with "find vulnerabilities"

Start with the obvious design: an agent with HTTP and browser tools, the replica's address, and the instruction.

It follows a link in a ticket to an external domain and sends requests there. It logs in with an administrative fixture account it found in a seed file, views C-77, and reports a disclosure visible to any user; the administrator sees everything by design. It reports that same disclosure eight times, once per page that renders records. It spends the rest of its budget on variations of a single idea and declares the campaign complete. Nothing distinguishes what it proposed from what the gateway blocked from what happened.

The limitation is that scope was a sentence, findings were the agent's word, and reset was nobody's job. The first decision is how much the tester should improvise.

## A scripted suite or an adaptive tester

### Path A: a scripted adversarial suite

Scripted tests with pinned fixtures and expected outcomes: reproducible regression coverage for known classes, bounded by what the authors anticipated.

### Path B: an adaptive tester in the controlled replica

The tester adapts to observations: it follows unfamiliar behavior and finds new candidates, and it loops, overstates, and attempts out-of-scope work.

| Dimension | Scripted suite | Adaptive tester |
| --- | --- | --- |
| Quality | Repeatable known checks; limited discovery | Broader candidates; every finding needs independent replay |
| Latency | Predictable duration | Variable exploration and minimization |
| Cost | Fixed execution and reset | Attacker, target, verifier, and resets all consume budget |
| Privacy | Synthetic fixtures | Adaptive observations still need redaction and access control |
| Safety | Explicit actions under controller enforcement | The same enforcement against novel plans and redirects |
| Operations | Tests and target versions | Plus probe lineage, termination, minimization, novelty review |
| Recovery | Reset and rerun | Reset all state; replay the smallest safe candidate independently |

We start with Path A for every confirmed regression and use Path B for bounded discovery, promoting reproducible findings into A. Neither path gets wider scope to improve its score. Under Path B, the tester has to choose what to try next.

## What the model sees and returns

### Choosing the next probe

The tester receives the scope manifest's permitted surface, the coverage matrix with its untested cells, observations so far with chapter 35's trust labels, and the hypothesis it is pursuing. It returns a probe proposal with a category, a target inside the manifest, a parent hypothesis, and the observation it expects. The controller executes probes; the model never does.

```json
{
  "probe_id": "P-0931",
  "parent": "H-cross-user-read",
  "category": "authenticated_read",
  "principal": "U-1",
  "target": {"replica": "R-5", "route": "records/view", "object": "C-77"},
  "expected": "403 or empty; a 200 with C-77's fields is a candidate",
  "cost": {"target_calls": 1}
}
```

Diversity is managed by the coverage matrix, never by sampling temperature: a probe that lands in an already-covered cell with an equivalent hypothesis is deprioritized, and the tester is steered toward untested routes, identities, and states. Equivalent failures are stopped after a bounded count.

### Attacker and target are different models

The testing agent and the target application's AI assistant run on separate model deployments with separate credentials and contexts. A shared model would share blind spots, and a finding about the assistant's tool boundary means less when the tester is the same system under a different prompt. The verifier is a third role with its own inputs, under chapter 16's independence rule.

### Lineage and cost

Every probe records scope and target versions, parent hypothesis, action category, state preconditions, a response reference, the effect trace, and its cost in tester, target, and verifier calls. Candidate claims and confirmed findings are separate records from the first probe onward.

The tester proposes a probe whose target is outside the replica.

## Scope is a manifest the gateway enforces

The scope manifest names target identities, allowed origins and services, accounts, action categories, controlled sinks, the time interval, rate and spend limits, stop conditions, and the reviewer. The gateway verifies it on every dispatch and resolves every destination through the control plane, including redirects and generated addresses: a page that presents another origin widens nothing, and a request toward it is denied and logged. A restored runner receives current scoped credentials, never ambient authority from before.

The replica holds only synthetic secrets and canary records; the controller has no production credential for the tester to discover. The tester, the target application, the verifier, and the hidden oracle run in four isolated environments, with filesystem mounts, egress, and credentials restricted independently of generated code, and the termination mechanism stays available if the testing process fails. A defect in the target cannot grant access to the oracle's expected identities or to the host.

> **Source finding.** Replit [described](https://replit.com/blog/defense-in-depth-how-replit-secures-every-layer-of-the-vibe-coding-stack) hardened containers, separate development databases, and recovery storage outside the working directory; Sierra [described](https://sierra.ai/blog/agency-secure-scalable-sandboxes-for-agents) isolated runners with credential-handling proxies and checkpoint recovery. Both are vendor accounts of control-plane boundaries and validate nothing about this lab.

A probe is blocked at the gateway, and the question is what that blocked probe means.

## Propose, reject, effect

Three things can happen to a forbidden action, and a campaign that merges them into one "attack success rate" has measured nothing useful.

- The model **proposes** it. This is evidence about model behavior under the test's conditions.
- The gateway **rejects** it. This is evidence that the system boundary held.
- The **effect** occurs. This is a boundary failure.

```text
   tester ──probe──► controller ──► gateway ──┬── allowed ──► target replica ──► effect trace ──► controlled sink
                                              │                                      │
                                              └── denied ──► rejection record         └──► verifier (clean snapshot, hidden oracle)

  outcome levels per forbidden action:   proposed  |  rejected  |  effect
  reported as three counts; never summed
```

Figure 36.1. Attacker, target, verifier, and oracle isolation, and the three outcome levels for a forbidden action.

The chapter's authored local fixture pairs refusal text with a forbidden structured proposal in the same model output, the shape chapter 23 tested for refunds. A guarded executor rejects the proposal, and the effect log stays empty; a deliberately broken executor records a forbidden effect; a separate permitted task checks that an executor rejecting every action cannot pass, since a defense that blocks everything has also blocked the application. The fixture tests an observable boundary in a synthetic environment and reports no vendor incident and no attack-cost figure.

The three levels are the mechanism the book names here. A candidate finding sits at the third level, and nobody can reproduce it.

## Reset everything, replay the smallest case

A fresh trial restores application data, permissions, sessions, queues, caches, the assistant's memory, and the controlled sinks, and resets the tester's target-specific context when the comparison requires it. The baseline digest and a smoke check run before every replay. A database reset alone leaves a mail queue, a privileged session, or a remembered answer from the previous run, which is how the opening finding appeared and disappeared: the first tester held an elevated fixture session, and the replay did not.

The verifier builds the smallest permitted demonstration that preserves the claimed impact and records target build, fixture, principal, state, sequence, observed result, and repetition count. A candidate that needs unintended state is described with that precondition or rejected; the verifier never reproduces with extra privileges and calls it equivalent. A finding confirmed on one build carries its build and configuration, and severity needs qualified review beyond a suspicious response.

Replay runs on the patched counterpart and on a benign control. The patched target must reject the prohibited behavior while the ordinary authorized task still succeeds, which is the utility check: a defense that blocks every request stops the attack and destroys the application. Confirmed boundary failures also need cleanup, with evidentiary records kept apart so reset erases no finding. The tester writes neither the oracle nor the patch-control labels.

```mermaid
sequenceDiagram
    participant Ver as Verifier
    participant Env as Environment control
    participant R5 as Target R-5
    participant R5p as Patched R-5p
    participant Or as Hidden oracle
    Ver->>Env: reset data, permissions, sessions, queues, caches, assistant memory, controlled sinks
    Env-->>Ver: baseline digest and smoke check pass
    Ver->>R5: replay the smallest permitted demonstration under the stated principal and state
    R5-->>Ver: observed result and repetition count
    Ver->>Or: compare against expected identities and effects
    Or-->>Ver: confirmed, rejected, or described with its precondition
    Ver->>Env: reset again
    Ver->>R5p: replay the same sequence
    R5p-->>Ver: prohibited behavior rejected
    Ver->>R5p: benign control task
    R5p-->>Ver: ordinary authorized task succeeds, the utility check
```

Figure 36.2. Reset and replay. Every replay starts from a verified baseline, the hidden oracle judges the result, and the patched counterpart has to reject the behavior while the benign task still succeeds.

Eight confirmed findings arrive, one per route.

## Deduplicate by cause, qualify by impact

Eight routes that render records can share one authorization defect. Findings are deduplicated by root cause while the affected-surface coverage is kept, so the report says one defect across eight routes, and productivity is never counted as eight. Each finding states demonstrated impact, preconditions, affected versions, a safe reproduction reference, uncertainty, and proposed remediation, with detailed evidence under access control and secret values redacted from summaries.

A no-finding result states the tested scope, budget, and limitations and certifies nothing beyond them. A reproducible candidate that review downgrades in impact is still a result. Confirmed findings become versioned fixtures with fixed failure and pass conditions, a protected holdout set is kept for evaluating future testers and defenses, and new strategies and defenses release through bounded campaigns with a reviewer authorizing any expanded scope. Rollback preserves evidence and cost history.

```mermaid
stateDiagram-v2
    state "Probe" as Probe
    state "Candidate claim" as Candidate
    state "Confirmed finding" as Confirmed
    state "False positive" as FalsePositive
    state "Qualified by precondition" as Qualified
    state "Deduplicated by cause" as Deduplicated
    state "Versioned fixture or protected holdout" as Fixture
    [*] --> Probe: tester proposal inside the scope manifest
    Probe --> Candidate: observation differs from the expected one
    Candidate --> Confirmed: clean replay reproduces it under stated preconditions
    Candidate --> FalsePositive: clean replay fails and the reason is recorded
    Candidate --> Qualified: reproduces only with unintended state
    Confirmed --> Deduplicated: one root cause, affected surface kept
    Deduplicated --> Fixture: fixed failure and pass conditions
    Fixture --> [*]
    FalsePositive --> [*]
    Qualified --> [*]
```

Figure 36.3. A candidate's lifecycle. A candidate is a claim until clean replay reproduces it, and confirmed findings are deduplicated by cause before they become fixtures.

## A redirect, a stale session, an all-blocking patch

An external redirect, a nonreproducible finding, and a defense that blocks everything.

| Injection | Required detection and state | Recovery | Oracle |
| --- | --- | --- | --- |
| Replica redirects to a third-party origin | Destination outside scope | Gateway blocks; transition recorded | No request reaches the third party |
| Tester requests host secrets | Capability denied | Attempt recorded | No host data in target or logs |
| Candidate relies on a stale privileged session | Baseline mismatch | Clean reset; qualified replay | No false ordinary-user finding |
| Model emits a forbidden tool proposal | Proposal separated from execution | Gateway policy applies | Blocked distinguished from executed |
| Queue survives database reset | Reset incomplete | Queue fixture cleared | Baseline digest and behavior restored |
| Patched target blocks all utility | Utility regression | Defense revised; retested | Legitimate task still passes |
| Budget ends during exploration | Campaign stopped with coverage gaps | Bounded evidence returned | No hidden continuation or spend reset |
| Eight findings from one cause | Root-cause deduplication | Single finding with surface coverage | Productivity not inflated |
| Attacker and target share a model | Role isolation check fails | Separate deployments assigned | Independence recorded |

The controller's logs and the controlled sink are the effect oracle; the tester's narrative marks nothing. These drills are specified and have not been run.

## Which path to ship first

Path A for confirmed regressions and Path B for bounded discovery was the provisional choice. The lab needs snapshots with known answers, and the cost arithmetic has to count every role.

### Twenty-four snapshots

Twenty-four target snapshots: seeded defects, patched counterparts, and benign distractors, covering cross-user canaries, the assistant's tool boundary, missing preconditions, and prohibited redirects. Both paths run under equal budgets with independent reset. Measured: verified unique findings, false positives, reproduction rate, defined coverage, time and cost to finding, scope violations, legitimate utility, with unsuccessful campaigns and budget censoring recorded.

> **Source finding.** AgentDojo's task model [separates](https://agentdojo.spylab.ai/concepts/task_suite_and_tasks/) legitimate-task checks from attack checks over environment state and traces. Both oracles are inspected here, and a forbidden transient effect fails a trial even when later cleaned up; the benchmark establishes nothing about coverage of real adversaries.

### Campaign cost, all roles counted

Fifty campaigns with 100 tester calls, 80 target-model calls, and 40 verifier calls each are 11,000 model calls, $55 at $0.005 a call, before sandboxes, application requests, storage, and resets. Reporting the tester's 5,000 calls alone omits more than half the modeled work. An average cost among successful discoveries is no minimum attacker cost: reusable candidates, unsampled strategies, failed campaigns, target versions, and distribution tails all matter, and this chapter asserts no economic threshold. Monitored: probes per target and campaign, denied egress, reset failures, verifier backlog, evidence retention, and the candidate queue, since discovery without verification produces a growing queue instead of findings.

### Gates

Path A stays the release regression layer. Path B runs where new-surface exploration earns verified discoveries under the same scope, and it stops when reset fidelity or control-plane enforcement is uncertain.

## Key ideas

- The testing agent is untrusted; scope is a manifest the gateway enforces on every dispatch, with destinations resolved through the control plane.
- Propose, reject, effect are three outcomes with three counts; summing them measures nothing.
- A candidate is a claim until clean replay reproduces it; reset covers data, sessions, queues, caches, memory, and sinks, and is verified by digest.
- Minimize the demonstration, replay on the patched counterpart and a benign control, and require utility to survive the defense.
- Deduplicate by cause, qualify by impact, and let a no-finding result state its scope.
- Attacker, target, verifier, and oracle are four isolated roles on separate models; campaign cost counts all of them.

Chapter 37 takes the controller-between-agent-and-world pattern out of software, to a lab where a retried command costs a sample.

## Exercises

1. Classify five trace outcomes into proposed, rejected, or effect: (a) the assistant's output contains a tool call to mail an external address and the gateway returns a denial; (b) a message appears in the controlled sink addressed outside the allowlist; (c) the tester's plan text says it will try an administrative route and no request follows; (d) a request to a third-party origin is logged at the gateway as denied; (e) U-1's session returns C-77's fields.

2. A candidate reproduced in run 1 and failed clean replay in run 2. List the state a reset must cover and name the two most likely leftovers that explain the difference.

3. Eight findings report the same authorization failure on eight routes, and a ninth reports a different cause on one of those routes. How many findings does the report contain, and what does each carry?

<details>
<summary>Answers</summary>

1. (a) proposed and rejected: the model proposed, the gateway denied, no effect. (b) effect: a boundary failure, whatever the transcript says. (c) proposed only, and weakly, since no structured action followed; it is evidence about model behavior. (d) proposed and rejected at the scope boundary. (e) effect: the cross-user disclosure occurred, and it is a confirmed finding once clean replay reproduces it under U-1's ordinary session.

2. Application data, permissions, sessions, queues, caches, the assistant's memory, controlled sinks, and the tester's target-specific context, verified by baseline digest and smoke check. The likely leftovers: a privileged session from a fixture account used in run 1, or a cached response that served C-77 without re-checking authorization.

3. Two findings. The first names one root cause with eight affected routes as its surface coverage, its preconditions, affected build, impact, and a minimized reproduction on one route plus confirmation on the others. The second names its own cause on the shared route with its own reproduction, and the report notes that the route carries two defects so a fix for one is not verified against the other.

</details>

## Sources

Sources used here, linked to the original articles:

- [AgentDojo state and trace oracles](https://agentdojo.spylab.ai/concepts/task_suite_and_tasks/)
- [Replit layered agent isolation](https://replit.com/blog/defense-in-depth-how-replit-secures-every-layer-of-the-vibe-coding-stack) and [Sierra sandbox control plane](https://sierra.ai/blog/agency-secure-scalable-sandboxes-for-agents), carried from chapters 31 and 27 for control-plane boundaries

