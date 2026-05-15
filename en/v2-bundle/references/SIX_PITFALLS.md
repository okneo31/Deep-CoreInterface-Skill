# SIX PITFALLS

> 📖 **Proverbs 22:3**
>
> "**The prudent see danger and take refuge, but the simple keep going and pay the penalty.**"
>
> A pitfall can only be avoided by those who recognize it. This document is for recognizing in advance the 6 pitfalls that destroy good code in the AI era. Only those who see them step aside.

Six patterns that destroy good code in the AI era, as identified in Matt Pocock's 410k-view talk "Software Fundamentals Matter More Than Ever."

This document is the baseline for all work.

---

## Pitfall ① The AI Builds Something Different From Your Intent

### Symptom
- "Just build it" → AI interprets it however → seemingly plausible result.
- Looks fine at first, but differs from what the user actually wanted.
- The cost of fixing afterward is far greater than getting it clear from the start.

### Cause
- The expectation that AI will figure things out without the user spelling out their intent.
- AI fills ambiguity with "plausible assumptions."

### Mitigation: Grill Me Approach
- **Before** writing code, the AI interrogates the user.
- Ask about intent, users, data format, edge cases, stopping conditions.
- Only when the answers are locked (ambiguity gone) does coding begin.
- Detailed question template: `GRILL_ME_PROTOCOL.md`

### TTL Application Example
- TTL Matgo "build AI coaching" → immediate coding forbidden. Interrogate first: "What kind of coaching? Real-time? After-game? Based on what data? Can the user dismiss it?" Only then begin.

---

## Pitfall ② Vague Specs

### Symptom
- "Make users like it"
- "Make it pretty"
- "Optimize it"

### Cause
- Spec-writing is tedious.
- Expectation that AI will handle even a vague spec.
- Often the requester themself doesn't know what they want.

### Mitigation: Spec Lock
- Before coding, specify:
  - **Input:** exact data structure and format
  - **Output:** return shape for both success and failure
  - **Exceptions:** when empty, null, or over-limit
  - **Success criteria:** unambiguous definition of "this is done"
- No coding without an agreed spec.

### TTL Application Example
- HOSU's "build VibeScore" → before Spec Lock:
  - Input: what data scores it? (survey? behavior? both?)
  - Output: score range? display format? private/public?
  - Exceptions: missing data? only one resident?
  - Success criteria: what should a resident *do* after seeing the score?

---

## Pitfall ③ The Death of Code Review

### Symptom
- AI produces code so fast that review is skipped.
- Codebase grows but nobody understands it anymore.
- Eventually even the AI can't touch it.

### Cause
- Humans can't keep up with AI's pace.
- Complacency: "AI wrote it, so it's probably fine."

### Mitigation: Conscious Review
- After each module, do **at least one conscious review.**
- Core question: "Will the me-of-six-months-from-now understand why this is written this way?"
- If not, don't add comments — **rewrite the code.**

### TTL Application Example
- During TTL Coin contract code review: "Will the me-of-six-months-from-now know why this reward function uses `ecrecover`?" If No → rewrite.

---

## Pitfall ④ Deep vs Shallow Modules (Most Important)

Source: John Ousterhout, *A Philosophy of Software Design*

Detailed judgment guide: see `DEEP_MODULE_REVIEW.md`.

### Quick Summary
- **Deep Module (good):** simple interface + rich internals. Example: Unix `read()` — one line to call, internally handles disk/network/pipe/socket.
- **Shallow Module (bad):** complex interface + thin internals. Example: a wrapper that merely calls another function, getter/setter-bloated classes.

### Criteria
- Does the calling code become shorter and clearer? → Deep
- Do you have to know the internals to use it? → Shallow

### Mitigation
- Ask the question every time you create a module/class/function.
- If Shallow → merge or delete.

### TTL Application Example
- When you feel the urge to "make a service class" in a Laravel controller — does that service actually add value, or just wrap the controller again (Shallow)?

---

## Pitfall ⑤ Mindless Dependency Addition

### Symptom
- "This library is great!" → immediately added.
- `package.json` / `composer.json` swells.
- A year later: security vulnerabilities, maintenance burden, CVE landmines.

### Cause
- Unaware of the real cost of a dependency.
- Short-term convenience returns as long-term debt.

### Mitigation: Three Dependency Questions
Before any external dependency, ask:

1. **Can I write this myself in 30 minutes?**
   - If yes, write it. One less dependency.

2. **Will this library still be alive in 5 years?**
   - Check GitHub stars, last commit, number of maintainers.
   - If doubtful, don't add it.

3. **If this disappears, is our product done? (Is it worth that much?)**
   - If core value, OK. If peripheral, reconsider.

### TTL Application Example
- In Flutter: "This UI library looks pretty." → must pass all three questions before adding.
- Same for Laravel packages.

---

## Pitfall ⑥ Lack of Design

### Symptom
- Just start coding without thinking.
- Six months later: an inconsistent mosaic.
- Even you don't know where anything is.

### Cause
- Design time feels like "waste."
- Pressure for fast deliverables.

### Mitigation: Daily Design Investment (Kent Beck)
- Don't pile up big refactors all at once.
- Spend **at least 30 minutes daily** on system design.
- Drawing diagrams, revisiting module boundaries, rethinking names — all are design activities.

### Kent Beck's Quote
> "Tidy First?" — Tidy before you code.
> Small daily tidying is more effective than a big refactor.

### TTL Application Example
- Every Monday morning, 30 minutes: redraw by hand the module structure of one ongoing project. The odd places reveal themselves.

---

## Anti-Patterns: The Opposite of All Six

The opposite of these six pitfalls is the **Dark Pattern.**

| Principle | Opposite dark pattern |
|-----------|----------------------|
| Grill Me | Screen flow that traps users without asking intent |
| Spec Lock | Deliberately vague terms/specs (auto-renewing subscriptions, hidden fees) |
| Conscious Review | Deliberate obfuscation so nobody can review |
| Deep Module | Deliberately Shallow design so users can't migrate (lock-in) |
| Dependency Review | Forced dependency entanglement (vendor lock-in) |
| Daily Design | Deliberate chaos maintenance |

These are fundamentally the "zero-sum take" game (see `PHILOSOPHY.md` for detailed analysis).
Effective in the short term, but they cannot create new dimensions (ㄱ~ㅎ).
Trapped forever in Level 1~2.

---

## One-Line Summary

> "A pitfall can only be avoided by those who recognize it. Those who don't, fall straight in." (cf. Proverbs 22:3)

---

## Sources

- Matt Pocock, "Software Fundamentals Matter More Than Ever" (2026, 410k views)
  - **Original talk (English):** https://youtu.be/v4F1gFy-hqg
  - **Korean commentary (AgentOS channel):** https://youtu.be/FOee3zb98wI
- Pocock's skill repository: github.com/mattpocock/skills
- John Ousterhout, *A Philosophy of Software Design*
- Kent Beck, *Tidy First?*
