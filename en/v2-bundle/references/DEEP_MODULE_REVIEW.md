# DEEP MODULE REVIEW: Judgment Checklist for Deep vs Shallow

> "**It is the glory of God to conceal a matter; to search out a matter is the glory of kings.**" — Proverbs 25:2
>
> The designer holds the glory of concealing complexity; the reviewer holds the glory of searching it out. Deep Module Review is the place where these two glories meet.

Source: John Ousterhout, *A Philosophy of Software Design*

Reference this document whenever you create or review a module/class/function.
Used at Step 3 (Module Design) and Step 6 (Review) of the workflow.

---

## Core Definitions

### Deep Module (good)
- **Simple interface + rich internals.**
- Users (other code that calls this module) get great functionality with minimal cognitive load.
- Analogy: A good tool has a simple handle but intricate inner mechanisms.

#### Canonical Example: Unix `read()` System Call
```c
ssize_t read(int fd, void *buf, size_t count);
```
- **Interface:** 3 parameters. Done.
- **Internals:** Handles disk / network sockets / pipes / terminals / virtual filesystems. Includes cache, permission checks, blocking, interrupt handling.
- The caller never needs to know any of that complexity.

### Shallow Module (bad)
- **Complex interface + thin internals.**
- The user carries all the cognitive load but gets little in return.
- Analogy: A tool with a complicated handle that doesn't actually do much.

#### Canonical Example: A Wrapper That Just Calls Another Function
```php
class UserService {
    public function getUserById($id) {
        return User::find($id);  // Just one more function call
    }
}
```
- The interface (name, parameters) grew but the internal value is 0.
- Just call `User::find($id)` directly instead.

---

## Judgment Checklist (Apply Every Time You Create a Module)

### Five Core Questions

#### Question 1: Does the calling code become shorter and clearer?
- **YES → Deep signal.** If the caller cleans up, the module added value.
- **NO → Shallow suspicion.** If the module's introduction made code grow, suspect.

#### Question 2: Do you need to know the internal structure to use it?
- **YES → Shallow signal.** A module you can't use without knowing its internals has failed at abstraction.
- **NO → Deep signal.** If the user doesn't need to care about internals, abstraction succeeded.

#### Question 3: Is the module's interface (public methods/parameters) large compared to its internal code?
- **Interface > internals → Shallow.** Five methods that are each 3 lines?
- **Interface << internals → Deep.** One method, 3 parameters, 100 lines inside?

#### Question 4: What happens if you remove this module?
- **Caller code becomes clearer → it was Shallow.** Remove it.
- **Complex code scatters across many places → it was Deep.** Keep it.

#### Question 5: Hearing the module's name, can the user predict exactly what's inside?
- **YES → Deep signal.** The interface conveys intent well.
- **NO → Rename or redesign.**

---

## Common Shallow Patterns (to avoid)

> 📖 **Matthew 21:19** (the cursed fig tree)
>
> "Seeing a fig tree by the road, he went up to it but **found nothing on it except leaves**... 'May you never bear fruit again!'"
>
> A Shallow Module is a fig tree heavy with leaves. The interface (the leaves) looks impressive, but there's no fruit (real internal value). The core question of module review compresses to one: **"Is this module only leaves, or does it bear fruit?"** Don't leave fruitless modules in place forever.

### Anti-pattern 1: Meaningless Wrapper
```typescript
function getUserName(user: User): string {
  return user.name;  // Just property access
}
```
→ Use `user.name` directly.

### Anti-pattern 2: Getter/Setter Bloat
```java
public class Config {
  private String host;
  private int port;
  private String username;
  // ... 20 fields
  public String getHost() { return host; }
  public void setHost(String h) { this.host = h; }
  // ... 40 methods
}
```
→ A data structure with public fields is often enough.

### Anti-pattern 3: Interface-to-Class 1:1 Mapping
```php
interface UserRepository {
    public function find($id);
    public function save($user);
}
class UserRepositoryImpl implements UserRepository {
    // Exactly 1:1 with the interface, only one implementation
}
```
→ Do you really need multiple implementations? Or is one class enough?

### Anti-pattern 4: Functions Split Too Small
```javascript
function isValidEmail(email) {
  return checkEmailFormat(email) && checkEmailDomain(email) && checkEmailLength(email);
}
function checkEmailFormat(email) {
  return email.includes('@');  // one line
}
function checkEmailDomain(email) {
  return email.split('@')[1].length > 0;  // one line
}
function checkEmailLength(email) {
  return email.length < 100;  // one line
}
```
→ Just keeping it all inside `isValidEmail` may be clearer.

### Anti-pattern 5: Excessive Layering
- Controller → Service → Repository → DAO → DB helper → ORM
- Does each layer truly add value, or is it there "because that's how it's done in textbooks"?

---

## Deep Module Patterns to Create

### Pattern 1: Hide Large Responsibility Behind a Simple Interface
- Good example: An HTTP client's `request(url, options)` — internally has connection pooling, retries, auth, cache, but the interface is simple.

> 📖 **Luke 7:7-8** (the centurion's faith)
>
> "**But say the word, and my servant will be healed**... For I myself am a man under authority, with soldiers under me. I tell this one, 'Go,' and he goes; and that one, 'Come,' and he comes. I say to my servant, 'Do this,' and he does it."
>
> The centurion's request "but say the word" is the theological archetype of interface/implementation separation. The caller (the centurion) throws a one-line command; he need not know the internal mechanism. He understood this because he lived inside a chain of command — i.e., the abstraction layer. When Jesus praised this faith with "I have not found such great faith even in Israel," He was praising the insight itself — that there is rich internal substance behind a simple interface.

### Pattern 2: Defaults Stay Simple, Options Provide Richness
- Good example: `fetch(url)` alone works; `fetch(url, {method, headers, body})` adds richness.

### Pattern 3: One Powerful Abstraction Implemented Precisely
- Good example: Redis's key-value model — simple interface (get/set/del) but rich internals (various data structures and persistence).

### Pattern 4: Absorb Repeated Patterns From Calling Code
- If many call sites repeat the same flow, absorb that flow into the module's internals.

---

## TTL Project Application Examples

### TTL Matgo: Game Rule Engine
- **Deep candidate:** `Game::naeda($card)` — simple interface; internally handles rule validation, score calculation, turn progression. (Following the Ubiquitous Language principle — keeping Korean hwatu terminology)
- **Shallow risk:** Each rule as its own class, externally composed — then the user must know rule ordering.

### HOSU: Payment Module
- **Deep candidate:** `Payment::charge($resident, $amount)` — PortOne V2 integration, retries, receipt issuance, notification all internal.
- **Shallow risk:** A class that just wraps the PortOne API once — then using PortOne directly is better.

### TTL Forge: Domain Adapter
- **Deep candidate:** `Forge::generate($domain, $prompt)` — internally applies different models/prompts/post-processing per domain (signage/architecture/gaming).
- **Shallow risk:** Separate functions per domain exposed externally — the user must write the domain branching themselves.

---

## Weekly Check (paired with Kent Beck's daily-design practice)

Every Monday, 30 minutes:

1. List the modules created last week.
2. Apply the five questions above to each.
3. For any module judged Shallow:
   - Merge, or
   - Delete, or
   - Redesign.
4. If even one is found, note it so the same mistake doesn't repeat the following week.

---

## One-Line Summary

> "A good module asks little of its users and gives much.
> A bad module asks much and gives little."
