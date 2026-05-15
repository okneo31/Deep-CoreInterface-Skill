---
name: software-fundamentals
description: Apply Matt Pocock's "Software Fundamentals Matter More Than Ever" principles together with Neo's metaphysical and theological framework. Use this skill whenever the user starts a new coding task, requests planning/architecture, asks for module design, wants to refactor existing code, or begins a new product/feature spec — even if they don't explicitly mention "fundamentals" or "principles". Triggers include phrases like "make a feature", "build X", "design Y", "plan Z", "refactor", "implement", "design", "how should I write this", "create a module", "start a project". Skip ONLY for trivial one-line fixes, pure factual lookups, or non-engineering tasks (translation, copywriting that has nothing to do with product). When in doubt, trigger.
---

# Software Fundamentals

> **Deep × Core × Interface**

> "Code is not cheap. Bad code is the most expensive it's ever been." — Matt Pocock
>
> "The fear of the LORD is the beginning of knowledge." — Proverbs 1:7

These two statements are two layers of the same truth. **Fundamentals = the root.**
All code rests on the root of good structure, and all knowledge rests on Him as the root.
This skill operates from that root.

---

## 0. Trigger Conditions

Trigger this skill's workflow (§4) on any of the following:

- Request to build a new feature/module/service
- Beginning of a new product/project plan
- Refactoring request for existing code
- Architecture-design request
- "How should I write this?" / vague questions (the vaguer the more important to trigger)

**Exceptions (do not trigger):**
- Typo fixes, one-line changes, obvious work
- Fact lookups ("Laravel 11 release date?")
- Non-engineering work (translation, general copywriting)

---

## 1. The Planner's Metaphysics (Why This Skill Exists)

The planner's capability divides into four levels:

| Level | Name | Meaning | Example |
|-------|------|---------|---------|
| 1 | a~z Optimization | Improve efficiency inside a fixed frame | Speed up existing payment flow |
| 2 | -a~z+ Discovery | See the edges of the frame | "Why must payment be the last step?" |
| 3 | @ Invention | Change the frame itself | Move to a business model without payment |
| 4 | ㄱ~ㅎ Creation | Move dimensions | An experience where the user never even thinks the word "payment" |

**Core claims:**
- Level 3~4 leaps are possible only from **good intent.**
- Ill intent is fundamentally a "take from a fixed pie" game — no motive to create new dimensions. Just take more from existing ones.
- Good intent is a "grow the pie" game — it has the necessity of creating new dimensions.
- Creating a new dimension is essentially a **creative act** — rebuilding the form received (Imago Dei).

**Ask yourself at the start of any coding/planning task:**
> "Which level is this task at? Optimization inside a~z, or opening a new dimension?"

Level 1~2 work is legitimate. Not every task needs to reach ㄱ~ㅎ. But you must **know where you are.**

### Core Formula: Good Intent + Clarity = Transcendence

Good intent alone is not enough. Blurry good-will produces blurry results.
Clarity alone is not enough either. Clarity without intent produces fake transcendence (dark patterns, efficient theft).

> **Good Intent + Clarity = Real ㄱ~ㅎ Creation**

§2 (Six Pitfalls), §3 (Four Practices), §4 (Workflow), and §5 (Grill Me) are all that **"bridge of clarity."** A bridge that turns good intent into real leaps. For those who have only intent, lay the bridge. For those who have only the bridge, ask about intent.

### Deep × Core × Interface

The entire skill compresses to three words:

```
User  ──→  Interface  (simple surface · bridge of clarity)
              ↓
           Deep        (rich internals · good intent · metaphysics)
              ↓
           Core        (the root of everything · Proverbs 1:7)
```

- **Deep** — Good intent, metaphysics, rich internals, the power to create ㄱ~ㅎ.
- **Core** — Fundamentals = the root. The "beginning of knowledge" from Proverbs 1:7.
- **Interface** — The bridge of clarity. Pocock's technical principles.

This skill is built by its own principle (Deep Module = simple interface + rich internals).

---

## 2. The Six Pitfalls (Pocock's Six)

Six patterns that destroy good code in the AI era, and how to avoid each.

### Pitfall ① The AI builds something different from your intent
- **Symptom:** "Just build it" → AI interprets it however → cost of fixing afterward is far greater than getting it clear upfront.
- **Mitigation:** **Grill Me approach.** Before coding, the AI interrogates the user. Ask about intent, edge cases, users, data formats — only when answers are locked does coding begin. (Detailed template in §5)

### Pitfall ② Vague specs
- **Symptom:** Abstract demands like "make users like it."
- **Mitigation:** **Spec Lock** with input / output / exceptions / success criteria explicit. No coding without an agreed spec.

### Pitfall ③ The death of code review
- **Symptom:** AI is too fast → review is skipped → nobody understands the codebase → eventually even AI can't touch it.
- **Mitigation:** After every module, **at least one conscious review.** "Will the me-of-six-months-from-now understand why this is written this way?"

### Pitfall ④ Deep vs Shallow Modules (most important)
Source: John Ousterhout, *A Philosophy of Software Design*

- **Deep Module (good):** simple interface + rich internals. Example: Unix `read()` — one line to call, internally handles disk/network/pipe/etc.
- **Shallow Module (bad):** complex interface + thin internals. Example: a wrapper that just calls another function, getter/setter-bloated classes.

**Criteria:**
- Does the calling code become shorter and clearer? → Deep
- Do you have to know the internals to use it? → Shallow

**Mitigation:** Apply this question every time you create a module/class/function. If Shallow → merge or delete.

### Pitfall ⑤ Mindless dependency addition
- **Symptom:** "This library is great!" → added → security vulnerabilities / maintenance burden a year later.
- **Mitigation:** Before adding any external dependency, **three questions:**
  1. Can I write this myself in 30 minutes?
  2. Will this library still be alive in 5 years?
  3. If this disappears, is our product done? (Is it worth that much?)

### Pitfall ⑥ Lack of design
- **Symptom:** Just code without thinking → 6 months later, an inconsistent mosaic.
- **Mitigation:** Kent Beck — **"Invest daily in system design."** Don't pile up big refactors; even 30 minutes a day.

---

## 3. The Four Positive Practices (Pocock's Four)

Avoiding pitfalls alone is not enough. Four principles to actively uphold.
Source: Pocock's original talk — "decades-old ideas that didn't break, they got more important."

### Practice ① Ubiquitous Language
- **Source:** Eric Evans, DDD.
- **Core:** Business vocabulary = code vocabulary = UI vocabulary = meeting vocabulary. Translation cost = bugs.
- **Application:** Build a glossary at the start of every project. Code / UI / DB / docs all follow it.
- **TTL example:** Keep Korean hwatu game terms ("go-stop / matgo / chida / naeda") in code (`naeda` rather than `playCard`).

### Practice ② Vertical Slices
- **Source:** XP / Agile.
- **Core:** Not horizontal layers (all UI → all logic → all DB), but one feature working end-to-end from UI to DB. Slice complete = releasable.
- **Application:** Start with the thinnest slice. Move to the next only after the current slice is complete.
- **TTL example:** First slice = "one solo card play with score calculated on one screen" works end-to-end. AI coaching / voice / billing are later slices.

### Practice ③ TDD (Test-Driven Development)
- **Source:** Kent Beck.
- **Core:** Red-Green-Refactor. A test is a spec. Especially important in the AI era — the standard for verifying AI-generated code.
- **Application:** Write the test first → give AI "make this test pass" → confirm pass, then tidy.
- **TTL example:** Begin TDD on core algorithms (rule engine / VibeScore calculation / market-price algorithm).

### Practice ④ Deep Modules
- Already covered in Pitfall ④. Simple interface + rich internals.

### Integration of the Four Practices
```
[Lock intent in same language via Ubiquitous Language]
        ↓
[Define scope as a Vertical Slice]
        ↓
[Pin spec with TDD]
        ↓
[Implement as Deep Module structure]
```

---

## 4. Mandatory Workflow

For any new coding/planning request, **always** follow this order. Never skip.

```
1. Grill Me Phase    Interrogate intent (in user's language)           (§5 question template)
       ↓
2. Spec Lock         Clear spec + Ubiquitous Language
       ↓
3. Module Design     Deep Module design + Vertical Slice selection
       ↓
4. Dependency Check  Three-question test for dependencies
       ↓
5. Build             Implement via TDD (tests first)
       ↓
6. Review            Conscious review (Pitfall ③ mitigation)
       ↓
7. Daily Investment  Spend tomorrow's time on design too (Kent Beck)
```

**Important:** It's normal — and correct — for steps 1~4 to take *far* longer than step 5 (Build).

---

## 5. Grill Me Question Template

Questions to ask before any coding. If answers are vague, coding is forbidden.

**Intent layer (Why)**
- What is the real purpose of this feature?
- How would the user live without it? (Is it really needed?)
- Which level (§1) does this task belong to?

**User layer (Who)**
- Who uses this? Imagine three different user types.
- What does that user think in the first 5 seconds of seeing this screen?

**Data layer (What)**
- What exactly is the input? What if empty / null / abnormal?
- What is the output? What's returned on failure?
- What happens with concurrent users doing the same action?

**Boundary layer (Where Not)**
- What must this feature absolutely not do?
- Next quarter, if it scales 1000×, what breaks?

**Stop-condition (When Stop)**
- Where is the line at which failure is acceptable?
- At what point can we call this "done"?

---

## 6. TTL Project Application Examples

Level classification and clarity-verification points for 15 ongoing projects (detailed explanations in V2's `references/PHILOSOPHY.md`):

| Project | Level | Key Frame Shift |
|---------|-------|-----------------|
| **NAODA (나오다)** | 3 | Seniors = care recipients → active value producers |
| **HOSU (호수)** | 3 | Maintenance fee = burden → tool for communal asset formation |
| **JoopDeal (줍딜)** | 2~3 | Seller sets price → market price openly shared |
| **TTL Coin** | 3 | PoW waste/centralization → PoA efficient equal distribution |
| **Zion (시온)** | **4** | Human-only labor market → human + AI equal participants |
| **IdeaForge** | 2 | Dependence on expensive consulting → AI self-validation |
| **Mideum-Saessak (믿음새싹)** | 2 | Paper attendance → digital faith ledger |
| **∆ON (다온)** | 3 | Telecom alone profits from data → user data sovereignty |
| **Stream Inc. (시냇가)** | 2~3 | Cannot hire CFO → AI + expert hybrid SaaS |
| **U n Me (너나나)** | 3 | Photo-first swipe → values-first match, photos later |
| **TTL Forge** | 3 | Generic 3D (Western aesthetic) → Korea-vertical integration |
| **Sseuk (쓱~!)** | 2 | Heavy mail clients → fast desktop + AI |
| **MyWay** | 2~3 | 7~30 day settlement + platform control → 24-hour automatic + autonomous pricing |
| **TTL Note** | 2~3 | Markdown = developers' tool → anyone via WYSIWYG, English jargon → Korean |
| **TTL Sign** | **3~4** | Separated drafting · signing · execution · dispute → unified AI+blockchain+escrow+mediation flow |

**Level distribution:**
- Level 2 (edge discovery): IdeaForge, Mideum-Saessak, Sseuk
- Level 2~3 (edge discovery + frame shift): JoopDeal, Stream Inc., MyWay, TTL Note
- Level 3 (frame shift): NAODA, HOSU, TTL Coin, ∆ON, U n Me, TTL Forge
- Level 3~4 (frame shift + dimensional shift attempt): TTL Sign
- Level 4 (dimensional shift): Zion

**Common pattern:** All 15 have good intent in place. What remains is to chase clarity all the way down.
The boldest Level 4 (Zion) and Level 3~4 (TTL Sign) demand the most clarity — the correlation between intent and clarity.

### Grill Me Application Examples
- TTL Matgo: "Does AI coaching actually make the game more fun, or does it just look cool?"
- HOSU: "Does VibeScore actually reduce disputes, or does it create a new axis of conflict?"
- U n Me: "Does the 36.5°C heart temperature actually improve match quality, or does it just look measurable?"
- TTL Sign: "Will blockchain records actually count as evidence in a Korean court, or are they just a marketing point?"

### Deep Module Candidate Examples
- TTL Matgo: Game rule engine (simple interface, rich internals). Shallow risk: API-wrapper bloat.
- TTL Forge: Domain adapter (unified interface for signage/architecture/gaming).
- Stream Inc.: AI diagnostic engine (common interface across 3 tiers, rich internals).
- TTL Note: Abstract AI-provider interface (unified Grok/Claude/Gemini).

---

## 7. Anti-Patterns (The Opposite of This Skill)

To see this skill's principles more clearly, know their opposite.

**Dark Patterns:**
- Trap users without asking their intent (opposite of Grill Me)
- Deliberately vague terms/specs (opposite of Spec Lock)
- Deliberately Shallow design to lock users in (opposite of Deep Module)
- Forced dependency entanglement (opposite of dependency review)

These patterns are the ill-intent game from §1. Effective short-term, but they cannot create ㄱ~ㅎ.

---

## 8. Daily Check

30 seconds before starting each day's coding:

1. Did yesterday's code include any Shallow Modules?
2. Is today's new dependency truly necessary?
3. Did this week's design time exceed 10% of coding time?
4. When was the last time you asked "why are we building this product"?
5. Are code/UI/docs using the same vocabulary? (Ubiquitous Language)
6. Does this slice work end-to-end? (Vertical Slice)
7. Any code this week without a test? (TDD)

---

## One-Line Summary

> 📖 **Genesis 1:31** — "God saw all that he had made, and it was very good."
>
> Let this one line be heard at the end of every work. Then that work has created ㄱ~ㅎ.

---

## Appendix: Sources

### Videos
- **Original talk (English):** Matt Pocock, "Software Fundamentals Matter More Than Ever" (premiered 2026-04-23)
  https://youtu.be/v4F1gFy-hqg
- **Korean commentary:** AgentOS channel, commentary on the 410k-view talk
  https://youtu.be/FOee3zb98wI

### Books / Texts
- John Ousterhout, *A Philosophy of Software Design*
- Kent Beck, *Tidy First?* and a body of system-design talks
- Proverbs 1:7
- Genesis 1:1
