# GRILL ME PROTOCOL: Intent Interrogation Template

> 📖 **Luke 14:28-30** (the parable of building the tower)
>
> "Suppose one of you wants to build a tower. **Won't you first sit down and estimate the cost** to see if you have enough money to complete it? For if you lay the foundation and are not able to finish it, everyone who sees it will ridicule you..."
>
> Writing code is building a tower. **Without sitting down first to count the cost,** you only lay the foundation and stop. Grill Me is the place of "sitting down first."

The step where, **before** writing any code, the AI interrogates the user.
Skipping this step lands you straight in Pitfall ① (the AI builds something different from your intent).

Only when answers are locked (ambiguity gone) do you move to the next step (Spec Lock).

---

## How to Use

> 📖 **Proverbs 20:5**
>
> "The purposes of a person's heart are **deep waters**, but one who has insight draws them out."
>
> The user's real intent lies in deep waters beneath the surface request. Under their "build X," real needs, hidden constraints, and unimagined edge cases lie submerged. The five layers of questions (Why/Who/What/Where Not/When Stop) are the buckets that draw out that deep water. Code built without drawing it out is only the surface X — not what the user actually wanted.

1. The moment the user says "build me X," open this document.
2. Ask **at least two questions per layer** (Why/Who/What/Where Not/When Stop).
3. If an answer is vague, ask again. **Stopping at this step is normal.**
4. Once all answers are locked, proceed to Spec Lock.

---

## Intent Layer (Why)

Question the real purpose of the task.

### Required Questions

- What is the **real purpose** of this feature?
- How would the user live without this feature? (Is it really needed?)
- Which level (§1 of PHILOSOPHY) does this task belong to?
- What value does this add to the company/product?

### Variant Questions (if needed)

- If we **don't** build this, what breaks?
- If competitors also have similar features, what makes ours different?
- Six months from now, if this feature failed — what would the reason be?

### Stop Signals (Refuse to proceed on vague answers)

- "It just feels like a nice-to-have" → STOP. Ask for the real reason.
- "Because competitors are doing it" → STOP. Does it fit *us*?
- "Users will probably like it" → STOP. Which users? What kind of "like"?

---

## User Layer (Who)

Concretize who will use this feature.

### Required Questions

- Who uses this feature? Imagine **three different user types.**
- What does that user think in the **first 5 seconds** of seeing this screen?
- What state was the user in just before using this feature? (time, place, emotion)
- What is this user's **hidden desire**? (the gap between what they say and what they really want)

### Variant Questions

- Who will absolutely *not* use this feature? Why?
- Does it work for the least skilled user?
- Is it enough for the most skilled user?

### TTL Application Examples

- TTL Matgo's "AI coaching": A beginner who needs a coach? A mid-level player checking their skill? An advanced player who loves data analysis? — Each may need a different screen.
- HOSU's "VibeScore": The resident seeing their own score? A neighbor seeing them? The management office? — Each interpretation differs.

---

## Data Layer (What)

Make I/O and exceptions explicit.

### Required Questions

- What exactly is the input? (type, format, range)
- What if it's empty/null/abnormal? Reject? Default? Error?
- What is the output? On success? On failure?
- What happens when multiple users do the same action concurrently?
- What if the data grows 1000×, 1,000,000×?

### Variant Questions

- Is the data source trustworthy?
- If this data comes from an external API and the API goes down?
- What if a user tries to tamper with it?

### Stop Signals

- "It usually comes in fine" → STOP. Specify what happens when it doesn't.
- "Just show the error" → STOP. Which error, shown how?

---

## Boundary Layer (Where Not)

Define what this feature **must not do.** Often the most important layer.

### Required Questions

- What must this feature **absolutely not do**?
- Where is the **boundary** with other features?
- Next quarter, if this feature scales 1000×, what breaks?
- If it malfunctions, what damage occurs? Is the damage reversible?

### Variant Questions

- Does this feature depend on others? Are those dependencies declared?
- If it touches other systems (payments, auth), what's the impact on those?
- Does it trap users? (dark-pattern check)

### TTL Application Examples

- TTL Matgo's payment: On payment failure, what's the game state? When is a refund possible? Underage payments must never go through.
- HOSU's dispute mediation: Mediation results must not be misinterpreted as having legal force.

---

## Stop-Condition Layer (When Stop)

Define when you can call it "done."

### Required Questions

- At what point can we call this **done**?
- Where is the boundary at which failure is acceptable?
- What can be **omitted** in the first release? What must absolutely not be?
- What goes in the next version?

### Variant Questions

- How will we measure success/failure of this feature?
- Check criteria at 1 week / 1 month / 3 months post-launch?
- If we end up killing this feature, what would the signal be?

### Stop Signals

- "Let's make it perfect" → STOP. Define perfect.
- "Just put everything in and we'll see" → STOP. Where's the boundary between core and peripheral?

---

## Final Audit

When all five layers are locked, confirm once more:

1. **Consistency:** Do the answers across layers contradict each other?
2. **Feasibility:** Is this possible within the given time/resources?
3. **Alignment with intent:** Do the Why answers match the What/Where Not answers?
4. **Ill-intent audit:** Does this feature stand on someone else's loss?

If all pass, proceed to Spec Lock.

---

## Anti-Patterns

> 📖 **Proverbs 18:13**
>
> "**To answer before listening — that is folly and shame.**"
>
> When the AI spits out code before fully hearing the user's story (intent, context, constraints) — that's "folly and shame." Quick replies look virtuous, but the cost of "answering before listening" is always greater.

Common traps at this step:

- **Skipping questions to start coding fast** → straight to Pitfall ①.
- **Not asking because the user might find it annoying** → bigger loss later.
- **Asking but moving on with vague answers** → vague spec locked in.
- **Expecting AI to fill it in** → AI fills ambiguity with "plausible assumptions."

Remember: **Standing still at this step is normal.** The stillness itself is value.

---

## One-Line Summary

> "Questions come before code. Only when questions are locked does code begin."
