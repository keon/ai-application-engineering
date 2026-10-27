# AI Application Engineering Book

This repository is the publishable edition of a case-based book about
AI-native applications. [README.md](README.md) is the entry point. The
writing workspace, with per-chapter briefs, reviewed source notes, course
notes, and planning documents, is a separate private repository; this edition
is generated from it, and edits to chapters should be made there.

## Start a session

1. Read [book/table-of-contents.md](book/table-of-contents.md) for the chapter
   order and status.
2. Read the chapter file in [book/chapters/](book/chapters/).
3. Each chapter's header names what it introduces, what it assumes, and what
   it reuses from earlier chapters; follow those for learning dependencies.

## Editorial scope

- Begin with a concrete application problem. AI is central to how the user
  creates, investigates, or executes work. Older AI features such as
  autocomplete are background or baselines.
- Assume existing models through APIs or hosted/open-weight deployments.
  Discuss model internals or training only when they change an application
  decision.
- Compare at least two credible implementation paths for the same case.
  Explain when each fits, quality, latency, cost, privacy, safety, operating
  burden, failures, recovery, and when to change paths.
- Teach retrieval, memory, tools, evaluation, routing, security, and runtime
  design inside application cases. Preserve the application-first titles.
- Distinguish documented source findings, our proposed design, illustrative
  arithmetic, and actual measurements. Never assign a proposed architecture to
  a company without evidence or turn an unrun test into a result.

## Writing

- Each chapter follows one structure: case,
  requirements ending in the naive version, two paths, model interface,
  build sections each opening from the previous one's limitation, failure
  drill, evaluation, key ideas, exercises, sources.
- Each case breaks one simplifying assumption and teaches three to five
  concepts it owns. Teach a concept in full only in its home chapter; elsewhere
  use a forward pointer or a named reference.
- Write in the voice described in [TONE.md](TONE.md) and run its checks.
- Mark each chapter `scaffold`, `draft`, or `complete` honestly. A polished
  draft is not complete without the promised design and evaluation evidence.
- Cite original primary sources, bounded and attributed. A product page,
  valuation, or search snippet does not establish system design.
