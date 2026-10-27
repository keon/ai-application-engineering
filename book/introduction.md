# Engineering Applications Where AI Is the Primary Interface

Status: opening draft; editorial framing. Updated: 2026-10-04.

[Table of contents](./table-of-contents.md) · [Chapter 1: Meeting notes that match the recording](./chapters/01-meeting-notes-that-match-the-recording.md)

A person leaves a meeting and expects usable notes. A developer describes a feature and expects a working change. A researcher delegates a question and expects a report whose conclusions survive scrutiny. In each case, the user supplies intent and context, then judges the application's work.

This book studies applications built around that interaction. Their central experience is generating, investigating, deciding, or executing with AI. A conversational interface is one possible surface; an editable document, a research matrix, a creative timeline, or an agent command center may be more useful. AI-native does not mean chat-only, and it does not require unrestricted autonomy.

## The Unit of Study Is an Application

We begin with a user and a job. What would count as a useful result? What may the application read or change? Which errors are tolerable, and which require a person to intervene? Only then do we compare models, tools, retrieval, workflows, and execution environments.

Most teams in these cases consume existing models through APIs or hosted/open-weight deployments. Model internals matter when they change an application decision. Pretraining and distributed training are not the organizing subjects.

The first case is a notetaker. A bounded recording-to-notes workflow introduces uncertain inputs, structured output, grounded claims, privacy, review, and evaluation. Later cases reuse these ideas in persistent knowledge, research, creative production, transactions, software changes, and coordinated agents.

## Every Case Makes a Choice

Each chapter compares at least two credible ways to solve the same problem. We ask when each path is appropriate, what it costs, how it fails, and how it recovers. A fixed workflow may be the right design. A bounded agent may be justified when the next step genuinely depends on discoveries. More agents are not a measure of maturity.

The recurring sequence is:

1. Define the application problem, requirements, and simpler baseline.
2. Compare candidate paths across quality, latency, cost, privacy, safety, operations, and recovery.
3. Walk through interfaces, data, state, authorization, and execution.
4. Inject a concrete failure and verify recovery.
5. Evaluate the result and decide what evidence would justify changing the design.

A useful answer is not always a completed task. A task that reaches the right final state can still have violated permissions on the way. Generated artifacts, external outcomes, and execution behavior therefore need separate evidence.

## How to Use the Book

Follow the numbered sequence to accumulate concepts, or use a chapter's dependency notes to reach a particular application. Media creation forms one branch; transactional work and software-changing systems form others. Security and evaluation begin immediately, even though specialized testing and investigation appear later.

Company examples help identify real product problems and alternative boundaries. They are not permission to invent private architectures. Throughout drafting, source-backed observations, illustrative assumptions, proposed designs, and measured results must remain visibly distinct.

All 38 chapter files are worked drafts: they develop the case, competing paths, state and authority contracts, failure recovery, and evaluation plans. Illustrative arithmetic is labeled as such. Application experiments remain unrun; empirical results and production lessons will be added only when supported by reproducible evidence or attributable primary sources.
