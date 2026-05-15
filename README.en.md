# Software Fundamentals

> **Deep × Core × Interface**

A Claude skill that integrates engineering fundamentals + a planner's metaphysics + theological root, designed to prevent the AI era from destroying good code while opening genuinely new dimensions.

> "Code is not cheap. Bad code is the most expensive it's ever been." — Matt Pocock
>
> "The fear of the LORD is the beginning of knowledge." — Proverbs 1:7

This skill operates from the awareness that these two statements are two layers of the same truth.

🇰🇷 [한국어 버전](README.md)

---

## What This Is

A Claude skill package that integrates the 6 pitfall-avoidance principles from Matt Pocock's 410k-view talk "Software Fundamentals Matter More Than Ever" with the 4 positive practices Pocock emphasized as "decades-old ideas that didn't break, got more important." On top of that, it integrates a **planner's metaphysics (a~z → -a~z+ → @ → ㄱ~ㅎ)** and the theological root of "the beginning of knowledge."

The core claim in one line:

> **Good Intent + Clarity = Transcendence**

Good intent alone produces blurry results. Clarity alone produces fake transcendence (dark patterns). Both together create real ㄱ~ㅎ.

---

## Who This Is For

- Developers who want to keep the fundamentals of their codebase intact in the AI era
- Planners who want to ask daily "is what I'm building now what should be built?"
- Anyone wanting a Claude Code skill that auto-triggers at the start of every coding request
- Those who believe engineering, metaphysics, and faith aren't separable

---

## Structure

Provided in two formats. Adopt whichever fits after review.

### V1: Monolith (single file)
```
v1-monolith/
└── SKILL.md
```
All principles compressed into one file. Fast trigger, simple management.

### V2: Bundle (core + references)
```
v2-bundle/
├── SKILL.md
└── references/
    ├── PHILOSOPHY.md         — Metaphysics + theological root
    ├── SIX_PITFALLS.md       — 6 pitfalls to avoid
    ├── CORE_PRACTICES.md     — 4 positive principles to uphold
    ├── GRILL_ME_PROTOCOL.md  — Intent-interrogation question template
    └── DEEP_MODULE_REVIEW.md — Deep/Shallow judgment checklist
```
Progressive disclosure structure. Each topic separated with depth.

### Korean Original
```
(repository root)
├── v1-monolith/SKILL.md
└── v2-bundle/
    ├── SKILL.md
    └── references/ (5 docs)
```

The Korean version is at the repository root; this English translation is under `en/`.

---

## Principles at a Glance

### 7-Step Workflow
```
1. Grill Me        Interrogate intent
       ↓
2. Spec Lock       Clear spec
       ↓
3. Module Design   Deep Module + Vertical Slice
       ↓
4. Dependency Check  Three-question test
       ↓
5. Build           Implement via TDD
       ↓
6. Review          Conscious code review
       ↓
7. Daily Design    Invest in system design daily
```

### Six Pitfalls (to avoid)
① AI builds something different from intent → Grill Me
② Vague specs → Spec Lock
③ Death of code review → Conscious review
④ Shallow Modules → Deep Modules
⑤ Mindless dependency addition → Three questions
⑥ Lack of design → Daily design

### Four Positive Principles (to practice)
① Ubiquitous Language — unify business/code/UI vocabulary (Eric Evans)
② Vertical Slices — one slice end-to-end (XP/Agile)
③ TDD — tests as specification (Kent Beck)
④ Deep Modules — simple interface + rich internals (John Ousterhout)

---

## Usage

### In Claude Code (most recommended)

```bash
# V2 bundle recommended
cp -r en/v2-bundle ~/.claude/skills/software-fundamentals/

# Or V1 single file
mkdir -p ~/.claude/skills/software-fundamentals
cp en/v1-monolith/SKILL.md ~/.claude/skills/software-fundamentals/
```

Claude Code automatically detects the trigger keywords in SKILL.md's description and follows the workflow at the start of any coding request.

### In Claude.ai

Integrate the SKILL.md content into your project's system prompt or memory, or attach it at the start of a new conversation with "please follow this skill."

### As General Reading

This repository itself can serve as a short book on principles of good code. Recommended reading order: PHILOSOPHY.md → SIX_PITFALLS.md → CORE_PRACTICES.md → GRILL_ME_PROTOCOL.md → DEEP_MODULE_REVIEW.md.

---

## Sources

### Videos
- **Original talk (English):** Matt Pocock, "Software Fundamentals Matter More Than Ever" (premiered 2026-04-23) — https://youtu.be/v4F1gFy-hqg
- **Korean commentary:** AgentOS channel — https://youtu.be/FOee3zb98wI

### Books / People
- Eric Evans, *Domain-Driven Design* (Ubiquitous Language)
- Kent Beck, *Test-Driven Development: By Example*, *Tidy First?*
- John Ousterhout, *A Philosophy of Software Design* (Deep Modules)
- XP (Extreme Programming) / Agile movement (Vertical Slices)
- Matt Pocock's GitHub Skills: https://github.com/mattpocock/skills

### Scripture
Proverbs 1:7, 18:13, 20:5, 22:3, 25:2 / Genesis 1:1, 1:31, 11:6 / Matthew 21:19 / Luke 7:7-8, 14:28-30 / Philippians 3:13-14 / 1 Thessalonians 5:21 / James 1:22

---

## One-Line Summary

> 📖 **Genesis 1:31** — "God saw all that he had made, and it was very good."
>
> Let this one line be heard at the end of every work. Then that work has created ㄱ~ㅎ.

---

## License

MIT License (proposed). Use, modify, and redistribute freely. Please maintain credit to the original source (Matt Pocock's talk).

---

## Author

**Neo (안재현)** · TTL Inc.

- Organized and extended Matt Pocock's talk principles in Korean
- Integrated planner's metaphysics (a~z → ㄱ~ㅎ) and theological root (Proverbs 1:7 / Genesis 1:31)
- Applied across 15 TTL ongoing projects

---

## Contributing

PRs welcome. Particularly seeking input in:
- Additional fitting scripture verse candidates
- Equivalent metaphysical analogies from other languages/cultures
- Project cases beyond TTL (your own cases as a contributing user)
- Polishing the English translation

Issues are also welcome.
