---
name: low-tech-design-review
description: Review or plan a product, feature, UI flow, or AI experience through a "calm, low-tech" lens inspired by early-2000s technology — orientation, useful friction, boundaries, and letting the user go. Use whenever the user asks to critique a design, audit an app or onboarding flow, reduce engagement-bait or dark patterns, make a product feel calmer or more humane, design notifications or AI assistants, or asks whether a feature respects attention — even if they don't say "calm" or "low-tech".
---

# Low-Tech Design Review

A hub skill for evaluating and shaping products so they help people do something and then get out of the way. It is the entry point for three companion skills that go deeper on each principle:

| Principle | Core question | Deep-dive skill |
|---|---|---|
| **Orientation** | Does the person know where they are, what's happening, and what comes next? | `orientation-design` |
| **Useful friction** | Is effort placed where it builds understanding and agency — and removed where it doesn't? | `useful-friction` |
| **Boundaries** | Does the experience have a clear beginning, a clear end, and easy exits? | `boundaries-and-exits` |
| **Letting the user go** | Does success mean the person accomplished something, rather than stayed longer? | `boundaries-and-exits` |

Cross-cutting qualities to look for everywhere: **attention regulation** (the product asks for the minimum attention needed), **slowness as a feature** (pacing that matches the task, not the metrics), **autonomy-first mechanics** (the person sets the goals and the pace), **real-world connection** (the product points back to life off-screen), and **gentle feedback loops** (signals that inform without nagging).

## Mental model: "a place you go" vs. "a place that follows you"

Early-2000s tech was mostly somewhere you *went*: a family computer in one room, a game with a save point, a CD-ROM with a menu. You arrived, did the thing, and left. Much modern tech is designed to be *ambient and sticky*: persistent, personalized, infinite, hard to put down.

The goal isn't nostalgia or worse tooling. It's to borrow the **legible shapes** of older tech — visible progress, finite sessions, explicit choices — and pair them with modern capability. This matters most for AI and always-on systems, where the default drift is toward invisibility and endless engagement.

## How to run a review

1. **Clarify scope.** Identify the flow, the primary user goal ("what did they come here to do?"), and the business metric it's currently optimized for. If any is unclear, ask one focused question before proceeding.
2. **Walk the flow as a session.** Narrate entry → task → completion → exit. Note every moment the person might feel lost, rushed, pulled sideways, or unable to leave.
3. **Score each principle** using the rubric below. Be concrete: cite the specific screen, component, copy, or behavior.
4. **Propose changes in tiers** — quick wins (copy, defaults), structural changes (flows, states), and strategic shifts (metrics, business model). Favor the smallest change that meaningfully helps.
5. **Name the trade-off** for each proposal (e.g. "may reduce DAU; likely improves retention-by-choice and trust").
6. **Suggest how to validate** — a small experiment, a metric that measures task success rather than time spent.

For detailed patterns while proposing fixes, consult the relevant companion skill.

## Rubric (0–3 per principle)

- **0 — Extractive:** actively works against the principle (hidden state, infinite feed, guilt-trip exits).
- **1 — Neglected:** no hostile pattern, but no intentional design either.
- **2 — Considered:** principle is addressed in the main path.
- **3 — Exemplary:** principle shapes the whole experience, including edge cases and failure states.

### Quick diagnostic questions

**Orientation**
- Can the person tell, at any moment, what the system is doing and how long it will take?
- Is system state (saved / syncing / AI thinking / queued) visible rather than implied?
- Is there a map — menu, steps, breadcrumb — or just a feed?

**Useful friction**
- Where does the product remove effort that the person would actually want (understanding, choosing, confirming)?
- Are irreversible or high-stakes actions slowed down appropriately?
- Is anything artificially slow or effortful *without* serving the user? (That's bad friction — remove it.)

**Boundaries**
- Is there a natural "done" state? Does the person get closure?
- Is the session finite by default (pages, chapters, daily limits) or infinite?
- Can they leave, pause, or unsubscribe as easily as they joined?

**Letting the user go**
- What's the success metric? Would it go up if the product got *better* at helping people finish faster?
- Do notifications serve the person's goals or the product's retention?
- Does the product ever point people back to the real world (offline action, other tools, a break)?

## Output format

```markdown
## Low-tech review: <flow name>

**User goal:** …
**Currently optimized for:** …

| Principle | Score | Evidence |
|---|---|---|
| Orientation | 2 | Upload shows % but AI step shows only a spinner |
| Useful friction | 1 | "Delete workspace" is one click, no summary |
| Boundaries | 0 | Infinite "suggested" feed after task completes |
| Letting go | 1 | Weekly digest emails default to on |

### Quick wins
- …

### Structural changes
- …

### Strategic shift
- …

### Trade-offs & how to test
- …
```

Keep the tone collaborative: this is a lens for making better trade-offs, not a purity test. Commercial products need to work commercially — the point is to find versions of success that don't depend on capturing more attention than the task requires.

## Anti-patterns to flag immediately

- Infinite scroll or autoplay after the user's goal is met
- Spinners with no indication of progress or duration for long operations
- Streaks, badges, or variable rewards that punish taking a break
- Confirm-shaming copy ("No thanks, I don't like saving money")
- Exits buried in settings; cancel flows longer than sign-up flows
- AI that acts silently, with no visible state or log of what it did
- Notifications defaulted on for non-essential events
