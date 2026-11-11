# AI Application Engineering

## Designing AI-Native Applications Through Cases

Working table of contents · Updated 2026-11-10.

The 30 applications below are the current chapter spine. Each chapter starts with a concrete application and compares at least two credible implementation paths. Evaluation, security, privacy, latency, cost, and recovery recur from the first case. Under each title, three lines give the failure the chapter opens with, the two paths it compares, and the system design it teaches.

Of the 30 chapters, 27 are drafts and three (3, 15, and 17) are scaffolds; none is marked complete or empirically validated.

## Introduction

[Engineering Applications Where AI Is the Primary Interface](./introduction.md)

- Intent, context, generated artifacts, delegated work, and human direction.
- How to read a case: requirements, alternatives, design, failure, evaluation, and evolution.
- What this book excludes: foundation-model training and a catalog of old applications with an AI feature.

## Chapters

### 1. [Meeting notes](./chapters/01-meeting-notes.md)

- A polished summary turns "do not ship Friday" into a commitment
- One call over the whole transcript vs extracting events and reconciling them
- System design: a validate-and-repair boundary around every model call; output items that carry references to their source spans; two state fields with different writers (what the conversation did, what the reviewer did); regeneration that arrives as a proposal beside reviewed work; evaluation against an answer key

### 2. [Brief from documents](./chapters/02-brief-from-documents.md)

- An amendment changes the notice period; the citation to the old clause is real and no longer governs
- Draft from the full packet vs build a claim ledger and assemble sections
- System design: a claim ledger as the intermediate record between sources and prose; four checks on every citation (exists, supports, applies, covers); a pinned source snapshot; approval bound to the exact bytes that will be delivered

### 3. [Knowledge-base answers](./chapters/03-knowledge-base-answers.md)

- The assistant answers a leave question from the 2023 policy because that page shares more words with the question than the page that replaced it
- Keyword search over whole pages vs chunked hybrid retrieval with a reranker
- System design (scaffold, not yet written): the indexing pipeline and how stale the index may be; hybrid retrieval, rank fusion, and reranking; a latency budget split across retrieve, rerank, and generate; retrieval recall measured apart from answer quality

### 4. [Thousand documents](./chapters/04-thousand-documents.md)

- A complete-looking results table hides a hundred files that failed to parse
- Read every review unit vs retrieve candidates and read selectively
- System design: fan-out to a pool of workers with leases and fenced publish; a scope certificate behind every "not found", over a matrix in which each required cell has an explicit state, including "failed to parse"; batch inference, prompt caching, and scheduling against tokens-per-minute limits; end-to-end quality as retrieval recall times extraction accuracy

### 5. [Team wiki](./chapters/05-team-wiki.md)

- A launch date is corrected, a name is ambiguous, and a revoked contractor can still read a cached page
- Scheduled snapshot synthesis vs incremental assertions and page projections
- System design: connectors that commit their cursor and their receipts in one transaction; incremental ingestion; two timelines per fact (when it was true, when we learned it); permission checks at delivery time; tombstones that carry a deletion to every derived copy

### 6. [Video event](./chapters/06-video-event.md)

- The top result shows the operator holding a filter; the real replacement falls between sampled frames
- Fixed-interval sampling vs content-aware sampling, with the same verifier
- System design: a media indexing pipeline with a sampling budget; mapping between stream, proxy, and asset clocks; a two-stage design where retrieval proposes candidates and a verifier confirms them; an evaluation that isolates sampling from verification

### 7. [Research agent](./chapters/07-research-agent.md)

- Five articles "corroborate" a claim that all trace to one vendor announcement
- A fixed search-read-synthesize plan vs a bounded adaptive investigator
- System design: the agent loop and its tool contracts; a budget ledger with reserved, spent, and uncertain amounts and a reserve for verification; stop rules written as code; context compaction; source independence counted by origin. Names Workflow vs Agent

### 8. [Data analysis](./chapters/08-data-analysis.md)

- A valid-looking join counts an order twice and the chart looks authoritative
- Curated analysis operations vs generated SQL and Python in a sandbox
- System design: sandboxed execution of generated code with caps on scans, runtime, and result size; grain and cardinality checks; an independent reconciliation calculation; promoting a generated query into a curated operation. Names Curated vs Generated

### 9. [Financial model](./chapters/09-financial-model.md)

- "Delay the hires and cut sales 10%" must become a precise patch to a model colleagues are changing
- Typed parameter edits to a fixed model vs generated extensions on an isolated branch
- System design: typed patches produced under a grammar; recalculation along a dependency graph; optimistic concurrency, where a patch is promoted against the version it expected and rebased when the head has moved

### 10. [Image studio](./chapters/10-image-studio.md)

- "Make the background blue" must leave the product label and the headline untouched
- Direct reference-conditioned generation vs generated components composited over protected layers
- System design: asynchronous provider jobs and results that arrive late; candidates and selection; a deterministic compositor around generated regions; mask coordinate spaces; a save that counts only when its hash is committed. Names Holistic vs Assembly

### 11. [Film shots](./chapters/11-film-shots.md)

- Changing the bicycle reference makes finished shots stale while a job using the old reference is still running
- One complete clip vs storyboard, per-shot generation, and deterministic assembly
- System design: a dependency graph of paid asynchronous jobs; computing which finished and running work a change invalidates; stale vs rejected as separate states; budgeted scheduling; preservation contracts stated in source bytes and in rendered bytes

### 12. [CAD parts](./chapters/12-cad-parts.md)

- "Make it narrower, keep each compartment 40 mm" can be impossible, and generated geometry can compile and still be wrong
- Validated parametric templates vs generated CAD operations in an isolated runtime
- System design: a generate-validate-repair loop with a deterministic verifier; a feasibility check before any generation; measurement after each operation; compiler repair kept apart from design repair; an export round trip

### 13. [Character memory](./chapters/13-character-memory.md)

- "My character has a brother" must not become a fact about the player, and a deleted detail must not resurface
- Recent dialogue with rolling summaries vs explicit state and scoped memory
- System design: scoped memory stores by kind; context assembly under a token budget; the model proposes a memory write and the application commits it; tombstones and generation checks that reject a late summarizer; deletion that reaches summaries and caches

### 14. [Resuming chat](./chapters/14-resuming-chat.md)

- A train enters a tunnel mid-answer and the workspace silently joins two different attempts
- Stream to the user with a provisional label vs buffer and check each unit before showing it
- System design: an append-only event log per attempt, committed before delivery; client cursors, replay, and gap detection; subscribing before reading to close the reconnect race; provisional output; cancellation; attempts kept apart from conversation history

### 15. [Model gateway](./chapters/15-model-gateway.md)

- One tenant's bulk import uses the whole tokens-per-minute allowance and every other tenant's chat fails
- A client library in each service vs a shared gateway that owns keys, quotas, routing, and metering
- System design (scaffold, not yet written): token-based rate limits and per-tenant quotas; routing by model tier and by prompt-cache affinity; fallback and hedged requests when every duplicate is billed; usage metered once across retries and cancelled streams

### 16. [Simulated users](./chapters/16-simulated-users.md)

- A simulated customer that knows the hidden order state, or accepts any "done", hides product failures
- Scripted user scenarios vs model-driven users in a controlled environment
- System design: an evaluation harness with information boundaries between simulator, application, and grader; graders that are themselves tested with known-bad runs; scenario and grader versions recorded together; invalid trials kept in the denominator

### 17. [Prompt release](./chapters/17-prompt-release.md)

- A prompt edit passes the offline suite, ships to everyone, and breaks a flow no test covered
- Gate on the offline suite and release to all vs staged release with shadow traffic, a canary cohort, and rollback
- System design (scaffold, not yet written): versioned prompt-and-model bundles; traffic splitting and assignment; online graders with sampled human review; regression detection by slice; rollback with in-flight conversations pinned to their version

### 18. [Exactly once](./chapters/18-exactly-once.md)

- The procurement system creates the request, then the worker crashes before saving the receipt
- An explicit graph with AI nodes vs a bounded planner at named exception points
- System design: durable workflow execution; a logical effect slot claimed before dispatch; an unknown outcome held until a lookup reconciles it; approval bound to a digest of the exact payload; replaying recorded model decisions instead of re-sampling them; compensation as a new action

### 19. [Moderation](./chapters/19-moderation.md)

- At a 0.1% base rate, a detector with 95% recall produces flags that are 91% false
- Rules and specialist checks with a review queue vs a policy-grounded contextual cascade
- System design: a classifier cascade sized by base-rate arithmetic; separate thresholds for detecting and for enforcing; review-queue capacity; a conditional write against the exact content version reviewed, with an outbox; four-state findings; appeals as reversal

### 20. [Refunds](./chapters/20-refunds.md)

- The refund commits, the reply vanishes, and a second chat asks "did you cancel it?"
- A dialog state machine vs flexible conversation with constrained execution
- System design: an operation identity derived from the case so two channels produce one operation; an operation ledger with a uniqueness constraint; reconciling the ledger before the model replies; bounded reservation of a balance, held while an outcome is unknown; a handoff that completes when a person accepts it; tests that read the effect log

### 21. [Phone bookings](./chapters/21-phone-bookings.md)

- "Actually, Wednesday" arrives while Tuesday's booking is committing
- Speech recognition, a text agent, and synthesis vs direct speech-to-speech with a separate action layer
- System design: a realtime audio pipeline with a latency budget per stage; turn detection; interruption epochs; ordering an interruption against an in-flight write; speculative reads on partial transcripts and no speculative writes; speech gated on the receipt

### 22. [Shopping agent](./chapters/22-shopping-agent.md)

- The navy bag sells out, a cheaper black one appears, and a payment may have gone through with no merchant response
- Research with manual checkout vs bounded integrated purchasing through verified merchants
- System design: a delegated grant with a cap, a cart digest, and an expiry; authorization, merchant commit, and capture tracked as separate effects; cumulative exposure reserved before dispatch; a substitution handled as a new proposal

### 23. [Job forms](./chapters/23-job-forms.md)

- Two yes/no fields swap places, a conditional question appears, and autosave sends data before "submit"
- Matching and drafting for the applicant to submit vs reviewed automated submission
- System design: driving an interface the application does not control; fingerprinting what was observed and reading back what was typed; a fact ledger behind every generated answer; grants for what may be disclosed during preparation; one submission slot

### 24. [Cross-app task](./chapters/24-cross-app-task.md)

- The issue is created, its response is lost, and a restricted customer detail must stay out of the team channel
- Reusable integration workflows vs a bounded general operator
- System design: permissions placed on data flows from a source to a destination; tool discovery under a context budget; an effect journal across several systems; honest partial completion; checkpoints that never cache authority

### 25. [Personal assistant](./chapters/25-personal-assistant.md)

- Two wakeups claim the same free hour while the user changes a preference and revokes calendar access
- Explicit event rules vs bounded proactive planning
- System design: event-triggered wakeups with a cheap gate before expensive planning; one decision key per proposal to suppress duplicates; grants stored apart from memory and read at dispatch; reservation of a time slot; a notification budget

### 26. [App builders](./chapters/26-app-builders.md)

- The preview is attractive, yet two members can reserve the same tool and a refresh loses the booking
- A constrained scaffold builder vs a general coding agent
- System design: a sandboxed build environment; acceptance tests stored where the agent cannot write; snapshots and recovery outside the agent's workspace; immutable release bundles; schema migrations at release

### 27. [Race condition](./chapters/27-race-condition.md)

- A slow request for document A overwrites the view after the user has switched to B
- A fixed reproduce-patch-test pipeline vs an adaptive coding agent
- System design: assembling repository context from search, a repository map, and language-server queries; deterministic reproduction with controlled completion order; a generation fence checked where a result is applied; compaction that keeps artifacts recoverable; re-running checks after the base moves

### 28. [Security alerts](./chapters/28-security-alerts.md)

- "sync-prod" and "Sam" may be different actors, and a log line asks the agent to export credentials
- A security playbook vs an evidence-driven investigator with a separate policy executor
- System design: trust labels by who could have written each field; an exposure graph whose edges carry freshness; identity links across namespaces; competing hypotheses with discriminating queries; an investigator that proposes and a separate executor that acts; containment as a conditional write

### 29. [Security testing](./chapters/29-security-testing.md)

- A candidate finding disappears after a clean reset, and a link points outside the replica
- A scripted adversarial suite vs an adaptive tester in a controlled replica
- System design: a scope manifest enforced at a gateway; an isolated replica reset to a known baseline; proposed, blocked, and actual effects counted apart; findings minimized until they reproduce

### 30. [Multi-agent](./chapters/30-multi-agent.md)

- The interface worker expects a string, the API worker returns an interval, and both report success
- A fixed graph with central scheduling vs an adaptive coordinator
- System design: an orchestrator over several workers; one owner per artifact, with fenced publish against an expected base; a parent budget that children draw from by reservation; completion levels that separate "each worker passed" from "the parts integrate"; cancellation that propagates; the human's view

## Working Notes

- The chapter order is authoritative here; keep filenames, chapter navigation, and dependency references synchronized when changing it.
- Company names are research lenses; no claim is made that their internal architecture matches our designs.
- Workload numbers, implementation results, and product capabilities remain unverified until supported by evidence.
