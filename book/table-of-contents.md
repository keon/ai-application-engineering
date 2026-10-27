# AI Application Engineering

## Designing AI-Native Applications Through Cases

Working table of contents · Updated 2026-10-25.

The 38 applications below are the current chapter spine. Each chapter starts with a concrete application and compares at least two credible implementation paths. Evaluation, security, privacy, latency, cost, and recovery recur from the first case. Under each title, three lines give the failure the chapter opens with, the two paths it compares, and the concepts it teaches.

All 38 chapters are drafts; none is marked complete or empirically validated.

## Introduction

[Engineering Applications Where AI Is the Primary Interface](./introduction.md)

- Intent, context, generated artifacts, delegated work, and human direction.
- How to read a case: requirements, alternatives, design, failure, evaluation, and evolution.
- What this book excludes: foundation-model training and a catalog of old applications with an AI feature.

## Chapters

### 1. [Meeting notes that match the recording](./chapters/01-meeting-notes-that-match-the-recording.md)

- A polished summary turns "do not ship Friday" into a commitment
- One call over the whole transcript vs extracting events and reconciling them
- Output schemas with a repair loop, grounding to utterances, discourse state vs review state, answer-key evaluation

### 2. [A brief from documents that disagree](./chapters/02-a-brief-from-documents-that-disagree.md)

- An amendment changes the notice period; the citation to the old clause is real and no longer governs
- Draft from the full packet vs build a claim ledger and assemble sections
- The four checks (exists, supports, applies, covers), positive vs scope dependencies, approving an exact revision

### 3. [Investigating a thousand documents when some won't parse](./chapters/03-investigating-a-thousand-documents-when-some-wont-parse.md)

- A complete-looking results table hides a hundred files that failed to parse
- Read every review unit vs retrieve candidates and read selectively
- Coverage accounting, retrieval recall times extraction accuracy, leases and fenced publish for parallel workers

### 4. [A team wiki that keeps up with its sources](./chapters/04-a-team-wiki-that-keeps-up-with-its-sources.md)

- A launch date is corrected, a name is ambiguous, and a revoked contractor can still read a cached page
- Scheduled snapshot synthesis vs incremental assertions and page projections
- Effective time vs knowledge time, permission-aware delivery, deleting derived copies

### 5. [Finding a short event in hours of video](./chapters/05-finding-a-short-event-in-hours-of-video.md)

- The top result shows the operator holding a filter; the real replacement falls between sampled frames
- Fixed-interval sampling vs content-aware sampling, with the same verifier
- Media clocks, candidate vs verified observation, separating sampling from verification in evaluation

### 6. [A research agent that knows when to stop](./chapters/06-a-research-agent-that-knows-when-to-stop.md)

- Five articles "corroborate" a claim that all trace to one vendor announcement
- A fixed search-read-synthesize plan vs a bounded adaptive investigator
- Source independence, budgets with uncertain spend, stopping rules; names Workflow vs Agent

### 7. [Data analysis over chat without double counting](./chapters/07-data-analysis-over-chat-without-double-counting.md)

- A valid-looking join counts an order twice and the chart looks authoritative
- Curated analysis operations vs generated SQL and Python in a sandbox
- Grain checks, independent reconciliation, descriptive vs causal claims; names Curated vs Generated

### 8. [Editing a financial model others are also editing](./chapters/08-editing-a-financial-model-others-are-also-editing.md)

- "Delay the hires and cut sales 10%" must become a precise patch to a model colleagues are changing
- Typed parameter edits to a fixed model vs generated extensions on an isolated branch
- Rate-basis and unit checks, dependency recalculation, promotion against an expected version

### 9. [An image studio that keeps the logo exact](./chapters/09-an-image-studio-that-keeps-the-logo-exact.md)

- "Make the background blue" must leave the product label and the headline untouched
- Direct reference-conditioned generation vs generated components composited over protected layers
- Deterministic vs generative edits, asynchronous provider jobs, late candidates; names Holistic vs Assembly

### 10. [Dubbing that keeps both timing and meaning](./chapters/10-dubbing-that-keeps-both-timing-and-meaning.md)

- Translated speech runs 3.8 seconds for a 3.2-second slot, and "do not reset" must stay a prohibition
- An integrated dubbing service vs an application-owned transcription, translation, synthesis, and mixing pipeline
- Sample-accurate timebases, voice authorization, regenerating only what a correction affects

### 11. [Replacing a chorus, keeping the verse](./chapters/11-replacing-a-chorus-keeping-the-verse.md)

- A new chorus must leave the verse and ending identical sample for sample
- Full-track regeneration and selection vs section generation with non-destructive assembly, with symbolic generation rendered to audio as a third path
- Musical time vs sample time, source vs rendered-sample preservation contracts, stem provenance, symbolic vs audio generation

### 12. [Regenerating only the shots affected by a change](./chapters/12-regenerating-only-the-shots-affected-by-a-change.md)

- Changing the bicycle reference makes finished shots stale while a job using the old reference is still running
- One complete clip vs storyboard, per-shot generation, and deterministic assembly
- A dependency graph of expensive asynchronous jobs, stale vs rejected shots, continuity across cuts

### 13. [Generating CAD parts that measure as specified](./chapters/13-generating-cad-parts-that-measure-as-specified.md)

- "Make it narrower, keep each compartment 40 mm" can be impossible, and generated geometry can compile and still be wrong
- Validated parametric templates vs generated CAD operations in an isolated runtime
- Constraint feasibility, kernel validation after each step, compiler repair vs design repair, export round trips

### 14. [A character that remembers, and forgets when asked](./chapters/14-a-character-that-remembers-and-forgets-when-asked.md)

- "My character has a brother" must not become a fact about the player, and a deleted detail must not resurface
- Recent dialogue with rolling summaries vs explicit state and scoped memory
- Five kinds of context, the model proposes and the application commits, correction and deletion lineage

### 15. [Resuming a chat response after a disconnect](./chapters/15-resuming-a-chat-response-after-a-disconnect.md)

- A train enters a tunnel mid-answer and the workspace silently joins two different attempts
- Stream to the user with a provisional label vs buffer and check each unit before showing it
- Attempts vs history, client cursors and replay, provisional output and cancellation

### 16. [Simulated users that can't cheat](./chapters/16-simulated-users-that-cant-cheat.md)

- A simulated customer that knows the hidden order state, or accepts any "done", hides product failures
- Scripted user scenarios vs model-driven users in a controlled environment
- Information boundaries, testing the grader, invalid trials that must not hide application failures

### 17. [Workflows that act on other systems exactly once](./chapters/17-workflows-that-act-on-other-systems-exactly-once.md)

- The procurement system creates the request, then the worker crashes before saving the receipt
- An explicit graph with AI nodes vs a bounded planner at named exception points
- Logical effect slots, unknown outcomes held until reconciled, approval bound to the exact payload, replaying recorded decisions

### 18. [Balanced invoices posted to the wrong company](./chapters/18-balanced-invoices-posted-to-the-wrong-company.md)

- Two similar suppliers, a $5 residual, and an entry that balances while booking the whole amount to the wrong category
- Deterministic matching with review vs a bounded discrepancy investigator behind the same posting gate
- Entity-scoped identity, atomic allocation of a payment, business duplicates, posting once

### 19. [Underwriting when evidence is missing or contradictory](./chapters/19-underwriting-when-evidence-is-missing-or-contradictory.md)

- Serial numbers differ between documents and a referenced attachment is absent; missing evidence must stay unknown
- Cited fact extraction with explicit policy rules vs a policy-grounded recommendation behind deterministic gates
- Four-state criteria, policy pinned by applicability, subgroup uncertainty, automation bias

### 20. [Marketplace moderation when most flags are wrong](./chapters/20-marketplace-moderation-when-most-flags-are-wrong.md)

- At a 0.1% base rate, a detector with 95% recall produces flags that are 91% false
- Rules and specialist checks with a review queue vs a policy-grounded contextual cascade
- Detection vs enforcement thresholds, acting on the exact content version reviewed, appeals and reversal

### 21. [Investigating a compliance alert when names collide](./chapters/21-investigating-a-compliance-alert-when-names-collide.md)

- Transfers link to an Alex Chen, and another Alex Chen works for a different supplier
- A fixed case-assembly workflow vs a bounded investigator with a question ledger
- Identity across namespaces, competing hypotheses, collection outcomes where a timeout differs from "nothing found"

### 22. [Claim appeals that take weeks and three channels](./chapters/22-claim-appeals-that-take-weeks-and-three-channels.md)

- The portal accepts the upload and times out before a receipt; a phone agent says the claim is still denied
- A versioned checklist workflow vs an adaptive case agent inside the same durable engine
- Line-level case state, deadlines vs reminders, submissions with unknown receipt, accepted handoffs

### 23. [Refunds over chat when the confirmation gets lost](./chapters/23-refunds-over-chat-when-the-confirmation-gets-lost.md)

- The refund commits, the reply vanishes, and a second chat asks "did you cancel it?"
- A dialog state machine vs flexible conversation with constrained execution
- Cross-channel operation identity, recovering the effect before the answer, testing effects instead of wording

### 24. [Phone bookings when the caller interrupts](./chapters/24-phone-bookings-when-the-caller-interrupts.md)

- "Actually, Wednesday" arrives while Tuesday's booking is committing
- Speech recognition, a text agent, and synthesis vs direct speech-to-speech with a separate action layer
- Interruption epochs, interruption linearized against dispatch, completion speech gated on the receipt

### 25. [A shopping agent allowed to spend but not substitute](./chapters/25-a-shopping-agent-allowed-to-spend-but-not-substitute.md)

- The navy bag sells out, a cheaper black one appears, and a payment may have gone through with no merchant response
- Research with manual checkout vs bounded integrated purchasing through verified merchants
- Delegated spending grants where slack under the cap is not permission, repricing under a merchant commit contract, payment vs order vs delivery as separate effects, substitution as a new proposal

### 26. [Filling in job application forms you don't control](./chapters/26-filling-in-job-application-forms-you-dont-control.md)

- Two yes/no fields swap places, a conditional question appears, and autosave sends data before "submit"
- Matching and drafting for the applicant to submit vs reviewed automated submission
- Fact ledgers that forbid invented qualifications, observation fingerprints with readback, preparation grants, submitting once

### 27. [One task across apps with different permissions](./chapters/27-one-task-across-apps-with-different-permissions.md)

- The issue is created, its response is lost, and a restricted customer detail must stay out of the team channel
- Reusable integration workflows vs a bounded general operator
- Data-flow permissions, partial completion reported honestly, checkpoints that never cache authority

### 28. [A personal assistant that works while you're away](./chapters/28-a-personal-assistant-that-works-while-youre-away.md)

- Two wakeups claim the same free hour while the user changes a preference and revokes calendar access
- Explicit event rules vs bounded proactive planning
- Grants kept separate from memory, cheap wake checks before expensive planning, notification budgets

### 29. [Outreach that stops the moment someone opts out](./chapters/29-outreach-that-stops-the-moment-someone-opts-out.md)

- A delayed follow-up is queued, the opt-out arrives first, and a sent message cannot be unsent
- An approved batch workflow vs a per-contact event-driven agent
- Evidence-backed personalization, suppression at the dispatch gate, sends bound to a communication obligation

### 30. [Campaign experiments when a variant loses its tracking](./chapters/30-campaign-experiments-when-a-variant-loses-its-tracking.md)

- One variant stops reporting conversions and the other "wins" by 140%
- A fixed production pipeline vs a controlled optimization agent behind an independent experiment controller
- Assignment, exposure, and outcome stored separately; frozen cohorts; peeking and delayed outcomes

### 31. [App builders where the preview works first](./chapters/31-app-builders-where-the-preview-works-first.md)

- The preview is attractive, yet two members can reserve the same tool and a refresh loses the booking
- A constrained scaffold builder vs a general coding agent
- Acceptance tests the agent cannot edit, recovery outside the agent's files, immutable release bundles

### 32. [Fixing a race condition in an existing codebase](./chapters/32-fixing-a-race-condition-in-an-existing-codebase.md)

- A slow request for document A overwrites the view after the user has switched to B
- A fixed reproduce-patch-test pipeline vs an adaptive coding agent
- Deterministic reproduction, a generation fence that holds even when abort fails, base drift before merge

### 33. [Migrating a live system while users keep writing](./chapters/33-migrating-a-live-system-while-users-keep-writing.md)

- A hidden automation emails customers for every imported contract, and decimal amounts must become integer cents
- A deterministic migration plan vs a discovery agent proposing validated steps
- Semantic mappings, change capture and catch-up, a fenced cutover, restore vs compensation vs forward repair

### 34. [Repairing a production incident on delayed telemetry](./chapters/34-repairing-a-production-incident-on-delayed-telemetry.md)

- The rollback targets a deployment another operator has already replaced, and silencing the alert would look like recovery
- A validated runbook vs adaptive investigation of competing hypotheses
- Discriminating queries, diagnostic load during an outage, blast radius and canaries, independent recovery checks

### 35. [Investigating security alerts with untrusted logs](./chapters/35-investigating-security-alerts-with-untrusted-logs.md)

- "sync-prod" and "Sam" may be different actors, and a log line asks the agent to export credentials
- A security playbook vs an evidence-driven investigator with a separate policy executor
- Provenance vs trustworthiness, presence vs reachability vs compromise, containment with residual risk

### 36. [Security testing with an untrusted agent](./chapters/36-security-testing-with-an-untrusted-agent.md)

- A candidate finding disappears after a clean reset, and a link points outside the replica
- A scripted adversarial suite vs an adaptive tester in a controlled replica
- Executable scope, proposed vs blocked vs actual effect, minimized and reproducible findings

### 37. [Lab experiments where a retry costs a sample](./chapters/37-lab-experiments-where-a-retry-costs-a-sample.md)

- After a sensor reconnects, cached readings look stable and the planner proposes another run
- Fixed recipes with model-assisted analysis vs a bounded adaptive planner behind a deterministic controller
- Acquisition freshness, non-repeatable commands, independent interlocks, selection bias in adaptive runs

### 38. [Agents whose work has to fit together](./chapters/38-agents-whose-work-has-to-fit-together.md)

- The interface worker expects a string, the API worker returns an interval, and both report success
- A fixed graph with central scheduling vs an adaptive coordinator
- Completion levels, artifact ownership and fencing, global budgets children cannot enlarge, the human view

## Working Notes

- The chapter order is authoritative here; keep filenames, chapter navigation, and dependency references synchronized when changing it.
- Company names are research lenses; no claim is made that their internal architecture matches our designs.
- Workload numbers, implementation results, and product capabilities remain unverified until supported by evidence.
