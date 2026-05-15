---
name: software-fundamentals
description: Apply Matt Pocock's "Software Fundamentals Matter More Than Ever" principles together with Neo's metaphysical and theological framework. Use this skill whenever the user starts a new coding task, requests planning/architecture, asks for module design, wants to refactor existing code, or begins a new product/feature spec — even if they don't explicitly mention "fundamentals" or "principles". Triggers include phrases like "make a feature", "build X", "design Y", "plan Z", "refactor", "implement", "design", "how should I write this", "create a module", "start a project". Skip ONLY for trivial one-line fixes, pure factual lookups, or non-engineering tasks. When in doubt, trigger.
---

# Software Fundamentals

> **Deep × Core × Interface**

> "Code is not cheap. Bad code is the most expensive it's ever been." — Matt Pocock
>
> "The fear of the LORD is the beginning of knowledge." — Proverbs 1:7

Fundamentals = the root. These two statements are two layers of the same truth.

---

## Core Workflow

When you receive any new coding/planning request, **always** follow this order:

```
1. Grill Me        Interrogate intent (in the user's language)   (→ GRILL_ME_PROTOCOL.md)
       ↓
2. Spec Lock       Lock the spec + Ubiquitous Language
       ↓
3. Module Design   Deep Module design + Vertical Slice selection  (→ DEEP_MODULE_REVIEW.md, CORE_PRACTICES.md)
       ↓
4. Dependency Check  Three-question test for dependencies
       ↓
5. Build           Implement via TDD                              (→ CORE_PRACTICES.md)
       ↓
6. Review          Conscious code review
       ↓
7. Daily Design    Invest daily time in system design (Kent Beck)
```

**It is normal — and correct — for steps 1~4 to take longer than step 5.**

---

## Trigger Conditions

| Trigger | Do not trigger |
|---------|---------------|
| New feature/module request | Typo fix |
| New project planning | One-line change |
| Refactoring request | Fact lookup |
| Architecture design | Translation / copywriting |
| "How should I write this?" / vague questions | Non-engineering work |

---

## Five Reference Documents

Read these as needed for depth:

| Document | Type | When to read |
|----------|------|--------------|
| `references/PHILOSOPHY.md` | Metaphysics | Before starting work, or when "why am I building this?" arises. Planner's metaphysics (a~z → ㄱ~ㅎ) and the source of the root. |
| `references/SIX_PITFALLS.md` | Avoidance (negative) | Baseline for all work. Pocock's 6 pitfalls and how to avoid them. |
| `references/CORE_PRACTICES.md` | Practice (positive) | The pair to SIX_PITFALLS. Ubiquitous Language / Vertical Slices / TDD / Deep Modules — 4 positive principles to uphold. |
| `references/GRILL_ME_PROTOCOL.md` | Tool | Question template for Step 1 (Grill Me). |
| `references/DEEP_MODULE_REVIEW.md` | Tool | Module-judgment checklist for Step 3 (Module Design) and Step 6 (Review). |

**Structure:** PHILOSOPHY is the root, SIX_PITFALLS + CORE_PRACTICES are the two wings (avoidance and practice), GRILL_ME + DEEP_MODULE are the tools held in hand.

---

## Daily 30-Second Self-Check

1. Did yesterday's code include any Shallow Modules? (`DEEP_MODULE_REVIEW.md`)
2. Is the dependency you'll add today truly necessary?
3. Did this week's system-design time exceed 10% of coding time?
4. When was the last time you asked "why are we building this product"?
5. Are code / UI / docs using the same vocabulary? (Ubiquitous Language)
6. Does this slice work end-to-end? (Vertical Slice)
7. Is there any code this week without a test? (TDD)

---

## Anti-Patterns (The Opposite of This Skill)

- Screens that trap users without asking their intent → opposite of Grill Me
- Deliberately vague terms/specs → opposite of Spec Lock
- Deliberately Shallow design to lock users in → opposite of Deep Module
- Forced dependency entanglement → opposite of dependency review

These patterns are fundamentally the "zero-sum take" game. They cannot create new dimensions. See `references/PHILOSOPHY.md` for the deeper reason.
