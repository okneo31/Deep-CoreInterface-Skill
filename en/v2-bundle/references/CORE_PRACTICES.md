# CORE PRACTICES: Four Positive Principles to Uphold

> "AI coding tools are overhyped and powerful at the same time... The devs who succeed aren't the ones who delegate everything or nothing. They're the ones who fall back on engineering fundamentals... **decades-old ideas that didn't break. They got more important.**" — Matt Pocock

If `SIX_PITFALLS.md` covers the **6 pitfalls to avoid**, this document covers the **4 positive principles to uphold.**
Avoiding pitfalls alone is not enough. Active practice principles must accompany.

From 18 months of teaching developers to build with AI agents, Pocock found the successful pattern: not those who "delegate everything" or "delegate nothing," but **those who fall back on engineering fundamentals.** Those fundamentals are these four.

---

## When to Apply

Where each principle enters the workflow:

| Step | Principles applied |
|------|--------------------|
| 1. Grill Me | **Ubiquitous Language** (ask in the user's vocabulary) |
| 2. Spec Lock | **Ubiquitous Language** (spec in the same vocabulary) |
| 3. Module Design | **Deep Modules**, **Vertical Slice selection** |
| 4. Dependency Check | (n/a) |
| 5. Build | **TDD**, **Vertical Slice execution** |
| 6. Review | **Deep Modules check** |
| 7. Daily Design | All four, daily self-check |

---

## 1. Ubiquitous Language

> 📖 **Genesis 11:6** (just before Babel)
>
> "The LORD said, 'If as one people speaking **the same language** they have begun to do this, then nothing they plan to do will be impossible for them.'"
>
> When language is unified, people can begin anything. The words used by business, code, users, meetings — all should point to the same thing. Where language scatters, no work ever reaches completion.

### Source
Eric Evans, *Domain-Driven Design* (DDD). The principle of unifying business-domain vocabulary with code vocabulary.

### Core Principle
- **Translation cost = bugs.** If users say "cancel order" but code says `cancelOrder`, UI says "void payment," and the database says `tx_void` — leakage will happen somewhere in those translations.
- **One word, one meaning.** If the same word points to different things across contexts (e.g., "user" — buyer at checkout, player inside the game, member in admin) — the boundary must be made explicit.
- **Language is discovered, not invented.** If users / domain experts already have a word, use that. Don't force a new term invented by engineers.

### Application
- At project start, **build a glossary first.** A standalone doc, not buried in a screen.
- Class/function names, UI labels, DB columns, docs — all follow the glossary.
- When a new term emerges, register in the glossary first, then reflect it in code.

### TTL Project Examples
- **TTL Matgo:** Keep Korean hwatu game terms ("고스톱" / "맞고" / "치다" / "낸다" / "쪼다") in code. Don't translate to English (`naeda` rather than `playCard`).
- **HOSU:** Get "관리비 / resident / dispute / group buy" agreed-upon meaning across users / management office / residents. Is VibeScore a "mood score" or a "community score"? Make it explicit.
- **JoopDeal:** Standardize secondhand-market terms ("market price / fair price / quick sale") — embed in code as users actually call them.

### Anti-Patterns
- Calling the same concept different things in code / UI / docs.
- Ignoring the user's word and forcing technical jargon ("transaction" instead of "payment").
- The same word means different things across contexts without that boundary being explicit.

---

## 2. Vertical Slices

> 📖 **Philippians 3:13-14**
>
> "...But one thing I do: **Forgetting what is behind and straining toward what is ahead**, I press on toward the goal..."
>
> One slice at a time. A small piece that goes from start to finish (the goal) in a single pass. Not 50% of everything at once — but a single slice taken to 100%.

### Source
XP (Extreme Programming) / Agile movement. Often illustrated: "Don't lay each brick layer by layer; build a small house first, then add another above it."

### Core Principle
- **Horizontal layers ✗:** Build all UI, then all logic, then all DB. Integration happens at the very end, and only then do problems appear. Too late.
- **Vertical slices ✓:** Make one feature work end-to-end — from UI to DB — first. Then move to the next feature. Each completed slice is releasable.
- **Aligns with YAGNI (You Aren't Gonna Need It).** Don't build ahead; build only what this slice needs.

### Application
- When planning a new feature, define the **thinnest possible slice** first. The full flow "login → dashboard → payment" in its simplest form.
- A slice is complete only when UI + business logic + data + tests all work.
- When a slice is releasable, move on to the next.

### TTL Project Examples
- **TTL Matgo:** First slice = "one solo card play with score calculated on one screen" works end-to-end. AI coaching, voice, billing are later slices.
- **HOSU:** First slice = "one resident checks their maintenance fee" end-to-end. VibeScore, dispute mediation are later.
- **JoopDeal:** First slice = "search one platform (e.g., Bunjang), show market price" end-to-end. Other platforms / premium tier are later.

### Anti-Patterns
- "Let's design the DB first" → 6 months later UI appears → only then business says "this isn't what we meant."
- "Frontend is done but backend isn't" → mosaic state.
- A slice that's too thick (e.g., "the whole payment system" — that's a phase, not a slice).

---

## 3. TDD (Test-Driven Development)

> 📖 **1 Thessalonians 5:21**
>
> "**Test them all; hold on to what is good.**"
>
> Testing first, holding (adopting) second. Don't adopt without testing. Whether the code came from AI or a human, the same applies. Verification comes first; adoption follows.

### Source
Kent Beck, *Test-Driven Development: By Example*. Famous for the Red-Green-Refactor cycle.

### Core Principle
- **Red:** Write a failing test first. (No code yet, so it fails as expected.)
- **Green:** Write the minimum code to pass that test.
- **Refactor:** Keep the test passing while tidying the code.
- **A test is a spec.** Tests express business requirements most precisely. Stricter and more verifiable than natural-language specs.

### Why It Matters Especially in the AI Era
- AI-written code needs a standard for verification. Eye-checking each one is impossible at scale.
- With tests, you can give AI a precise spec: "Implement so this test passes."
- Without tests, AI-generated code piles up as "plausible-looking but actually broken."

### Application
- Start each feature by **writing the test first.** Code in your test: "Returns X on success, throws Y on failure."
- When asking AI to write code, **send the test with it**: "Implement to pass this test."
- Every slice (§2) includes tests. A slice without tests = not done.

### TTL Project Examples
- **TTL Matgo:** Begin with TDD on the rule engine core. Write dozens of tests like "this card combination → this score" first, then implement the engine.
- **HOSU:** Begin with TDD on the VibeScore calculation. "This data → this score" tests first.
- **JoopDeal:** Begin with TDD on the price-calculation algorithm. "This listing data → market price should be N won" tests first.

### Anti-Patterns
- "It's urgent, just code first, tests later" → "later" never comes.
- Tests exist, but were written after the code (tests written to match implementation are not specs).
- Asking AI for code only, not for tests → AI's code is unverified.

---

## 4. Deep Modules

This principle has its own dedicated document.

→ See **`DEEP_MODULE_REVIEW.md`.**

In one line: **simple interface + rich internals.** This was the principle Pocock emphasized most among the four, requiring its own separate judgment checklist — hence its dedicated document.

---

## Integration of the Four Principles

These four are not applied separately — they work **together.**

```
[Lock user intent in the same language with Ubiquitous Language]
            ↓
[Define scope as a Vertical Slice]
            ↓
[Pin the slice's spec with TDD]
            ↓
[Implement as Deep Module structure]
```

Without one, the other three weaken:
- **Without unified language** — slice definitions blur, tests don't know what they're verifying.
- **Without slice units** — tests become too big or too fragmented.
- **Without TDD** — no way to verify whether the Deep Module is actually deep.
- **Without Deep Module** — no clean unit to test.

The four principles are one system.

---

## Weekly Self-Check

Every Monday, 30 minutes, on one ongoing project:

1. **Ubiquitous Language:** Are there words in this week's code/docs/UI that don't match the glossary?
2. **Vertical Slices:** Did what you built this week work end-to-end, or only the middle?
3. **TDD:** Is there any code this week that went in without a test?
4. **Deep Modules:** Any Shallow modules this week? (→ the 5 questions in `DEEP_MODULE_REVIEW.md`)

If even one answer isn't No, that's next week's first task.

---

## One-Line Summary

> 📖 **James 1:22**
>
> "**Do not merely listen to the word, and so deceive yourselves. Do what it says.**"
>
> Avoiding pitfalls (SIX_PITFALLS) is the domain of "the listener." That alone is not enough. The four positive principles are the domain of "the doer." The one who has heard must do. Avoidance without doing is self-deception.

---

## Sources

### Videos
- **Original talk (English):** Matt Pocock, "Software Fundamentals Matter More Than Ever" (premiered 2026-04-23)
  https://youtu.be/v4F1gFy-hqg
- **Korean commentary:** AgentOS channel, commentary on the 410k-view talk
  https://youtu.be/FOee3zb98wI

### Books / People
- Eric Evans, *Domain-Driven Design* (original source of Ubiquitous Language)
- Kent Beck, *Test-Driven Development: By Example*
- John Ousterhout, *A Philosophy of Software Design* (original source of Deep Modules)
- XP (Extreme Programming) and Agile movement (origin of Vertical Slices)
