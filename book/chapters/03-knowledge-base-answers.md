# Chapter 3. Knowledge-base answers

Status: scaffold. Case framing and design plan only; the chapter is unfinished and unvalidated. Updated: 2026-11-10.

[Previous: Chapter 2](./02-brief-from-documents.md) · [Table of contents](../table-of-contents.md) · [Next: Chapter 4](./04-thousand-documents.md)

**New in this chapter:** chunking; embeddings and hybrid retrieval with rank fusion; reranking; retrieval recall measured apart from answer quality; abstaining when no retrieved passage supports an answer.

**Assumes:** a fixed corpus that every asker may read; one question per call; no conversation history. Later chapters remove these assumptions: sources that change and permissions that differ in chapter 5, and memory across turns in chapter 13.

**Reuses:** grounding to source spans and answer-key evaluation (chapter 1); the four checks on a citation (chapter 2).

> **About the examples.** The company handbook, its pages, and every number planned for this chapter are fictional.

## The case

An employee asks the handbook assistant how many weeks of parental leave they have. The handbook holds two pages on the subject: the 2023 policy and the 2025 policy that replaced it. The assistant answers from the 2023 page, because that page shares more words with the question. The citation is real and the answer is out of date.

Chapters 1 and 2 handed the model its evidence. Here the application has to find the evidence first, among a few thousand pages, and the answer can only be as good as what retrieval returns. The application answers questions with citations. It does not edit the handbook, and it says so when no page supports an answer.

## The two paths

Path A is keyword search over whole pages, with the top results placed in the prompt. Path B splits pages into chunks, retrieves with both keyword and embedding search, fuses the two rankings, and reranks the candidates before the model reads them. The chapter will compare them on the same question set, with retrieval recall and answer correctness reported as separate numbers.

## What the chapter will build

The planned sections follow the limitations in order: a page too long to place in the prompt whole (chunking); a question that shares no words with its answer (embeddings and fusion); a correct passage ranked twentieth (reranking); a fluent answer built from the wrong passage (recall measured apart from answer quality); and a question the handbook does not cover (abstaining).

The system design it will cover: the indexing pipeline and how stale the index may be, the latency budget split across retrieve, rerank, and generate, and what can be cached.

The fixture, the two paths, the failure drill, and the evaluation plan are still to be designed.

Chapter 4 keeps retrieval and the four checks and removes the assumption that the evidence fits in one call, with a thousand documents and a hundred that will not parse.

## Sources

No source has been reviewed for this chapter yet.

