# Tone of Voice

This file describes how the book sounds. It applies to the introduction, every chapter, and any prose a reader will see. Chapter briefs and source notes are working documents and can be terser, but they should still avoid the patterns in the "Patterns to avoid" section.

Read it before writing or revising a chapter. [AGENTS.md](AGENTS.md) covers what goes in a chapter; this file covers how it reads.

## Who we are writing for

Picture a software engineer two or three years into their career. They have shipped web services, used a relational database, and called a model API from a script. They have not yet built an application where the model's output becomes something people rely on. They are smart and short on time. They will try the exercises if the exercises are good.

Write for that one person. When a paragraph would only make sense to someone who already knows the answer, rewrite it for them.

## How the book sounds

The book sounds like a senior colleague working through a design at a whiteboard with you. They start with a concrete problem, draw the parts, try the obvious design, show where it breaks, and fix it. They say what they would choose and why. They admit what nobody has measured yet, once, plainly, and move on. Each section starts from a limitation of the design so far, stated in technical terms.

Use "we" for the design work the reader and author do together ("we store the transcript revision with each item"). Use "you" for direct advice ("validate every response in code"). Avoid "I" in chapters; the preface is the place for personal history.

Prefer plain words. Keep technical terms, because readers need them to search and to talk to colleagues, and define each one the first time it appears. Write in the present tense for designs and the past tense for what a source reported ("Circleback reported moving recording into native engines").

Be confident where the evidence supports it and specific where it does not. "Start with Path A" is a recommendation. "Path A works for meetings under ninety minutes in our fixture; longer meetings are untested" is a scoped claim. Both are better than a sentence that hedges in every clause.

## Patterns from exemplary tech writing

The sixteen patterns below come from technical articles that engineers still pass around years after publication. Each entry names the technique, points to the passage where an exemplar uses it, and says how this book applies it. Read the originals; our descriptions are summaries in our own words. To respect the authors' copyright, this file quotes only one short phrase and otherwise points to the passage.

### 1. One running example carries the whole piece

Brandur Leach's [idempotency-keys article](https://brandur.org/idempotency-keys) (2017) builds every concept on a fictional ride-sharing app, Rocket Rides, so each new table, state, and failure belongs to a system the reader already knows. Jacqueline Xu's [online migrations post](https://stripe.com/blog/online-migrations) (Stripe, 2017) does the same with the history of one data model, the Subscriptions object. Hamel Husain's [evals post](https://hamel.dev/blog/posts/evals/) (2024) draws its whole method from one real assistant, Rechat's Lucy.

In this book, every chapter has one fixture, introduced in its requirements section and reused by every later section and by the exercises. A new section never switches to an unrelated example.

### 2. Show it broken, say so, then fix it

Martin Kleppmann's [distributed-locking post](https://martin.kleppmann.com/2016/02/08/how-to-do-distributed-locking.html) (2016) presents a plausible lock-and-write routine under the label “THIS CODE IS BROKEN”, shows the pause that breaks it, and only then introduces fencing tokens. The reader meets the failure before the name of the fix.

In this book, a section that shows a failing design says so before the reader studies it ("The simplest design, which fails in the next few sentences, asks for a summary"). The failure comes from the fixture. The mechanism follows, then a sentence the reader can reuse.

### 3. Draw the failure as a timeline the reader can check

Kleppmann lays out the race as numbered steps for two clients beside a diagram. Kyle Kingsbury's Jepsen report on [Amazon RDS for PostgreSQL 17.4](https://jepsen.io/analyses/amazon-rds-for-postgresql-17.4) (2025) walks through one cycle of four transactions and the order of the writes each one saw, so the anomaly can be verified by hand.

In this book, races, retries, and stale results are shown as numbered steps or a small timeline figure with times or sequence numbers. A reader should be able to point at the step where things go wrong.

### 4. Let each design step follow from a stated limitation

Strong technical explanations move in a chain. They start with the naive approach and state its limitation in technical terms: what it costs, what it fails to guarantee, or which input breaks it. The next step adds the mechanism that removes that limitation, then states what the mechanism still leaves uncovered. Each step exists because of a specific limitation of the previous one, so the reader always knows why the next mechanism is there.

Kleppmann's locking post moves this way, from a lock, to its failure under a process pause, to fencing tokens, to whether Redlock can generate them. Brooker's backoff article does the same with measured contention.

Keep the chain technical. Transitions state a property of the design ("The validator checks that every cited utterance exists. This item passes it:"). They do not describe scenes, invent events ("after a few hundred meetings, responses start failing"), or report how users reacted. A failure is shown with the fixture, derived from the mechanism, or cited from a source. If none of those is possible, leave the step out.

In this book, a chapter keeps its template sections. The requirements section ends with the naive version and its limitation, and each later section opens from a limitation of the design so far. Chapter 1 is the worked example.

### 5. Build the argument as a ladder of experiments

Marc Brooker's [exponential backoff and jitter](https://aws.amazon.com/blogs/architecture/exponential-backoff-and-jitter/) (AWS, 2015) moves from no backoff to backoff to jittered backoff, and each graph exposes the limit of the previous idea. His conclusions describe what the simulation showed, and he links the simulator.

In this book, a design grows in steps the reader can follow, and each step is motivated by a weakness the previous step revealed. Where we have arithmetic or a simulation, the claim states what it covers.

### 6. Replay the failure list against the finished design

After building the system, Brandur's article lists the ways a request can go wrong, such as dropped connections and crashes partway through, and then replays each case against the design in a section that assumes the worst. Each case is stated as a condition, followed by how the system responds.

In this book, the failure drill does the same with the chapter's fixture, in a table of injected condition, detection, and required end state.

### 7. Lead with the verdict and scope it exactly

The Jepsen RDS report states its finding in the opening summary, then pins it to specific versions, endpoints, and test conditions. It also says which anomalies it did not observe and what testing cannot prove.

In this book, a comparison ends with a recommendation, and every claim carries its scope once, where it is made: which fixture, which workload, which assumption. Later sentences do not re-hedge it.

### 8. Separate what is documented, observed, and assumed

Dan Luu's [Files are hard](https://danluu.com/file-consistency/) (about 2015) separates what papers measured, what documentation guarantees, and what developers believe, and says when a man page relies on rumor. The Jepsen report compares observed behavior against PostgreSQL's documented isolation levels.

In this book, source findings, our proposals, illustrative numbers, and measurements are kept visibly apart, using the callout styles in the chapter template.

### 9. Define terms by the decision they change, then say when to use each

Erik Schluntz and Barry Zhang's [Building effective agents](https://www.anthropic.com/engineering/building-effective-agents) (Anthropic, 2024) defines workflows and agents by who controls the next step: predefined code or the model. Every pattern then gets a short paragraph on when to use it, and the article recommends starting with the simplest option.

In this book, a definition says what the distinction changes in the design. Each path in a comparison gets a "when it fits" paragraph and the observation that would make you switch.

### 10. Give a recurring idea a short, memorable name

Simon Willison's [lethal trifecta](https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/) (2025) names a combination of three agent capabilities, defines each in a line, and ties the warning to dated, linked incidents. The name makes the risk easy to raise in a design review.

In this book, each pattern a later chapter will reuse gets a name in its home chapter ("fenced publish", "answer-key evaluation", "Read Everything vs Intermediate Record"). We use the name, unchanged, from then on.

### 11. Give every pattern the same internal shape

Eugene Yan's [Patterns for building LLM-based systems](https://eugeneyan.com/writing/llm-patterns/) (2023) treats each pattern in the same order: what it is, why it matters, and how to apply it. The Stripe migration post introduces a four-step pattern and then applies it in four sections that mirror the list.

In this book, every chapter follows the chapter template, and every build-it section moves from failure to mechanism to rule, so readers learn where to look.

### 12. Show the real artifacts

Husain's evals post shows the tests, prompt templates, dashboards, and spreadsheets the team used. Brandur shows the full schema and code, with prose around each block that says what to notice.

In this book, each chapter shows at least one real artifact at readable size: the prompt, the output schema, the record, or the query. A sentence before or after it says what to look at.

### 13. Use arithmetic to make scale concrete

The Stripe migration post makes its case for parallel processing with a small calculation: at one second per object, a migration of that size would take years. Brandur uses basic probability at high request volumes to show why rare failures become daily events.

In this book, workloads come with arithmetic a reader can redo, and the result is used to make a decision.

### 14. Disagree generously

Kleppmann praises Redis and its author before criticizing the algorithm, limits the critique to locks used for correctness, and invites readers to form their own view. The Jepsen report stays factual, gives users practical workarounds, and credits the vendor's engineers in its update.

In this book, we criticize designs and claims, name what a source does well, and stay generous to the people behind them.

### 15. Let the headings carry the argument

Brooker's backoff article uses short headings that mark each stage of the argument, so the list of headings reads as a summary of the case being made. Brandur's failure-replay section takes its title from Murphy's Law, which tells the reader what kind of section it is before they start it. Kleppmann's headings name the step the argument has reached, such as making the lock safe with fencing.

In this book, a reader who skims only a chapter's headings should learn the case, the comparison, and the main lessons. Chapter 1's headings move from a summary that reversed a decision, through two ways to turn a transcript into notes, to the two places the Friday error can enter.

### 16. Start concrete and introduce one idea at a time

Julia Evans's [Patterns in confusing explanations](https://jvns.ca/blog/confusing-explanations/) (2021) lists what makes explanations hard to follow, including starting abstract, introducing too many concepts at once, unrealistic examples, and unsupported claims. Her [post on simple explanations](https://jvns.ca/blog/2020/11/15/simple-explanations-without-sounding-condescending/) (2020) adds two habits: keep enough jargon that readers can search for more, and anchor each idea in a real problem.

In this book, a chapter owns three to five new concepts, and a section introduces one. Technical terms stay, and each is defined the first time it appears. Use her list as a review checklist for every draft.

## Habits

### Back every claim

A claim needs a worked example from the fixture, arithmetic the reader can check, or a linked source. If none is available, say the claim is our proposal or an open question.

### Name a concept once and keep the name

Do not rotate synonyms to avoid repetition; readers assume a new word means a new idea. Bold a term the first time it is defined, and only then.

### Say what you recommend

End a comparison with a choice and the evidence that would change it. "Start with Path A. Switch to Path B if the retraction fixtures fail on long meetings" helps a reader more than a table that leaves the decision open.

### Scope a claim once

State the limits of a claim where it is made. Say once near the top of a chapter that its people and numbers are fictional.

### Sentences and paragraphs

Most sentences should be medium length and declarative, with the subject and verb near the start. Use a short sentence when a point needs weight. Keep paragraphs to one idea, usually two to five sentences. Write each step of a process as its own sentence or list item; a sentence with three clauses joined by semicolons usually wants to be a list.

### Humor and asides

A dry aside is welcome when it makes the example more real, as Brandur's jokes about Rocket Rides do. Keep humor out of failure drills, safety boundaries, and anything involving real people's money, health, or data. Keep jokes kind to the reader.

### Companies and sources

Name the company, the author when known, and the date. Report what the source says in the past tense and in our own words. Say what the source supports and stop there. Add a limit only when a reader would plausibly over-read the source. If a source contributes nothing beyond a disclaimer, remove the citation.

For the habits this book should avoid, the community-maintained Wikipedia page [Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) is the most thorough catalog. Its authors present the list as observations, and human writers show these habits too. In this book we treat the patterns below as defects to fix wherever they appear.

## Patterns to avoid

Each pattern below is common in text generated by language models and weakens technical writing. The "Before" examples are real sentences from earlier drafts of this book.

### Contrast framing

This is the pattern to watch most closely. It comes in several shapes:

- "not X, but Y" and "not just X, but also Y"
- "X, not Y" at the end of a sentence
- "It isn't X. It's Y." across two sentences
- "Y rather than X" when nobody proposed X
- "more than X: it's Y"

The shape implies that someone believed X. Usually nobody did, and the sentence spends half its length on a claim the reader never held. State Y directly and give it the detail it deserves. When a real misconception exists, say who holds it, show the evidence against it, and then give the better design in a separate sentence.

Before: "AI is central here because the job is interpretation, not search."

After: "AI is central here because the job is interpretation: tracking who proposed a date, who agreed, and who withdrew it forty minutes later."

Before: "A source link says where to look, not that the conclusion is right."

After: "A source link tells the reviewer where to look. Whether the passage supports the claim is still the reviewer's decision."

Before: "The worker owns a computation, not the reviewed notes."

After: "The worker owns its computation. The reviewer owns the accepted notes, and a late worker result arrives as a new proposal."

### Quotable closers

A paragraph that ends on a balanced aphorism ("A schema makes errors inspectable; it does not make them disappear.") sounds wise and teaches little. End on the last useful fact or instruction. Keep one memorable line per chapter at most, and make it a positive statement the reader can apply, such as "Completeness has a scope."

### Reflexive groups of three

Lists of exactly three adjectives, nouns, or clauses ("fast, reliable, and scalable") usually appear because three sounds finished. Use the number of items the subject actually has.

### Inflated vocabulary

Remove words that assert importance without adding information: crucial, pivotal, robust, seamless, powerful, cutting-edge, landscape, delve, leverage (as a verb), underscore, showcase, foster, testament, tapestry, game-changer. Replace "serves as", "acts as", and "boasts" with "is" and "has".

### Trailing -ing clauses

Sentences ending in ", ensuring reliability" or ", highlighting the need for review" attach a vague consequence to a concrete statement. Cut the clause, or turn it into its own sentence with a specific claim.

### Throat-clearing and signposting

Delete openers that only announce what comes next: "It's worth noting that", "Importantly,", "Let's dive in", "In this section, we will", "As we saw above", "Let's take a step back". Start with the point.

### Setups and reveals

Avoid "Here's the thing:", "The catch?", "The answer is simple:", and a question followed by a one-word answer. A single question is fine when the following paragraph answers it with substance, as Brooker and Kleppmann do.

### Section-ending recaps

Do not end sections with "In short," "The takeaway," or a sentence restating the section. The chapter has a Key Ideas list for that.

### Bold and label overuse

Bold a term once, where it is defined. Apart from the three header lines at the top of a chapter and the labels on callouts, do not start paragraphs or list items with bold labels such as "The failure." or "Key point:". The chapter template's build-it order (failure, mechanism, rule) describes how to sequence the prose. Write it as ordinary paragraphs.

### Em dashes

Use a period, comma, colon, or parentheses instead. Em dashes in running prose have become a recognizable tell, and the alternatives are almost always clearer. Status lines and table cells that use a dash as a placeholder are exempt.

### Hedge stacking

"May potentially", "can in some cases", "it is possible that this might" all spend words without adding a condition. State the condition ("on recordings with overlapping speech") or state the claim plainly.

### Vague attribution

"Many teams find", "experts agree", and "it is widely known" need a name and a link, or they should become our own stated view ("we recommend").

### Narrative framing

Scene-setting and invented events make a design read like a story at the cost of accuracy: "We will build it the way most teams do", "The output looks good, and that is the trouble", "Reviewers start editing, and their edits expose a flaw", "Run this across a few hundred meetings and things start to go wrong." State the technical property instead. "A schema stated in the prompt describes the expected output; nothing enforces it" says the same thing and claims nothing unmeasured.

### Template residue

Remove any sentence about the writing process itself: review history, notes on what a previous draft said, placeholder text, or reminders about what a source does not prove. That material belongs in the chapter brief. The technical resource approval checklist at the end of each chapter is the exception: keep it as written.

## Conventions

- Section headings tell the reader what the section shows or what goes wrong in it, in the terms of the case: "A real citation can still be wrong", "Two places the Friday error can enter". A skim of a chapter's headings should retell its argument. Role names such as "Requirements and baseline" or "Failure drill" belong in the template only. Key ideas, Exercises, and Sources keep fixed names so readers can find them.
- Headings use sentence case. Chapter and part titles keep title case. Sections are unnumbered; refer to another section by linking its heading.
- Numbers: spell out one to nine in prose; use digits for measurements, money, percentages, and anything compared in arithmetic. Show units every time ("9,720 tokens", "45 minutes").
- Dates use the form "October 13, 2026" in prose and ISO format (2026-10-13) in records and code.
- Every chapter's people have names no other chapter uses.
- Figures are numbered by chapter and captioned with a period ("Figure 1.2. The review workspace"). The caption is a line after the figure. Two figure forms are used: a ```text block for timelines, ledgers, and matrices where exact columns matter, and a ```mermaid block (flowchart, sequenceDiagram, or stateDiagram-v2) for component flows, races, and state machines. Mermaid labels with punctuation are quoted; diagrams stay under about 25 nodes; a diagram shows only what the chapter's prose says, using the chapter's own identifiers.
- Code, schemas, and prompts that are our proposals say so once in the surrounding prose.
- Put each source link on the claim it supports.

## Before submitting a chapter

Read the chapter aloud, or at least the first paragraph of every section. Then check:

1. Does each section open with something concrete from the running example?
2. Does every new term have a definition at first use, and is it used consistently afterwards?
3. Does every claim have an example, arithmetic, or a source?
4. Does every comparison end with a recommendation?
5. Is each limitation stated once, where it applies?
6. Is the chapter free of the patterns above?

A quick mechanical pass catches the most common patterns. Run it from the repository root and read every hit; some will be legitimate.

```sh
f=book/chapters/01-meeting-notes-that-match-the-recording.md
grep -nE ', not (a |an |the |just |only |merely )?[a-z]' "$f"
grep -nE "\bnot (just|only|merely|simply)\b|\brather than\b|isn't .*\. It's" "$f"
grep -n '—' "$f"
grep -niE '\b(crucial|pivotal|robust|seamless|powerful|landscape|delve|leverage|underscore|showcase|foster|testament)\b' "$f"
grep -nE "It's worth noting|Importantly,|Let's dive|In this section|Here's the thing|The takeaway" "$f"
```
