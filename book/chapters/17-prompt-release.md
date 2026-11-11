# Chapter 17. Prompt release

Status: scaffold. Case framing and design plan only; the chapter is unfinished and unvalidated. Updated: 2026-11-10.

[Previous: Chapter 16](./16-simulated-users.md) · [Table of contents](../table-of-contents.md) · [Next: Chapter 18](./18-exactly-once.md)

**New in this chapter:** versioned prompt-and-model bundles; shadow and canary traffic; online grading with sampled human review; regression detection by slice; rollback, with conversations in flight pinned to the version they started on.

**Assumes:** an application already in production with real traffic; changes are to prompts, tool descriptions, and model versions, with no training.

**Reuses:** answer-key evaluation and slices (chapter 1); simulated users and test the grader (chapter 16); routing by model tier (chapter 15).

> **About the examples.** The support assistant, its traffic, and every number planned for this chapter are fictional.

## The case

A team edits the support assistant's prompt to fix how it words refund denials. The offline suite passes and the change ships to all users. The cancellation flow, which no test in the suite covers, now refuses valid requests, and nothing reports it until the complaints arrive.

Chapter 16 evaluated an application before release. Here the application is already running, and a prompt or model change is a deployment whose effect is statistical: the same input can pass on one run and fail on the next. The release system decides who sees a new version and when to pull it back. It does not decide what the prompt should say.

## The two paths

Path A gates on the offline suite and then releases to everyone. Path B releases in stages: shadow traffic first, then a small cohort, with online graders and an automatic rollback rule. The chapter will compare them on the refund-and-cancellation fixture, including the cost of the traffic that Path B evaluates twice.

## What the chapter will build

The planned sections follow the limitations in order: a prompt edited in place with no record of what changed (versioned bundles); a regression outside the test suite (shadow traffic scored by online graders); a grader that drifts from human judgment (sampled review); an average that hides one failing flow (slices and repeated trials); and a rollback that changes behavior in the middle of a conversation (version pinning).

The system design it will cover: how traffic is split and assigned, how much traffic a cohort needs before a difference can be seen, where grader results are stored, and what triggers a rollback.

The fixture, the two paths, the failure drill, and the evaluation plan are still to be designed.

Chapter 18 removes the assumption that nothing leaves the application: a workflow's tools write to another system, and an action has to happen exactly once.

## Sources

No source has been reviewed for this chapter yet.

