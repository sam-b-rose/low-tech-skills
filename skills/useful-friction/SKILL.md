---
name: useful-friction
description: Decide where to add, keep, or remove friction so effort builds understanding and agency instead of being optimized away — pauses before irreversible actions, meaningful choices, intentional pacing (slowness as a feature), and autonomy-first mechanics. Use whenever the user is designing confirmations, onboarding, AI auto-actions or autocomplete, one-click flows, defaults, settings, purchase or delete flows, learning tools, or asks "should this be seamless?" or "is this too much friction?".
---

# Useful Friction

"Frictionless" became the default goal of product design. But removing *all* effort also removes the moments where people understand what's happening, make a real choice, or notice they didn't want to do something. Older tech had built-in pauses — waiting for a page, choosing from a menu, saving manually — and those pauses gave people a beat to think.

The aim isn't to make things harder. It's to **place effort deliberately**: remove it where it's waste, keep or add it where it creates understanding, agency, or safety.

## Good friction vs. bad friction

| Bad friction (remove) | Useful friction (keep or add) |
|---|---|
| Re-entering information the system already has | Reviewing a summary before an irreversible action |
| Artificial waits or dark-pattern mazes to cancel | A short pause before sending a message in anger |
| Unclear errors that force guessing | Choosing settings explicitly instead of opt-out defaults |
| Required fields that don't serve the user | Typing a confirmation for destructive actions |
| Slow tools that make people wait for no reason | AI suggestions the person accepts, not AI actions that just happen |

**Test:** Does this effort serve the *person's* goals (understanding, intention, safety, learning)? If it only serves the business, or nobody, it's bad friction.

## Patterns

### Pause before the irreversible
Delete, send, publish, purchase, share externally: show *what will happen* in concrete terms (counts, recipients, totals) and require a deliberate action. Undo is often better than confirm — offer it where possible.

### Choice over default
For anything affecting privacy, notifications, spending, or data sharing, ask instead of assuming. A one-time, well-explained choice beats a hidden opt-out.

### Suggest, don't act (autonomy-first)
With AI and automation, default to **proposals the person accepts** (diffs, drafts, previews). Escalate to auto-action only for low-stakes, reversible tasks the person has explicitly delegated.

### Slowness as a feature
Match pace to the task, not the metric:
- Reflective or creative tools can deliberately slow down (one prompt per day, a writing session timer, batch delivery of messages).
- Learning tools should make people do the thinking first, then reveal.
- Feeds and inboxes can arrive in batches rather than a constant stream.

### Effort that teaches
Small amounts of effort build mental models: arranging your own dashboard, naming your own folders, choosing which data to include. Don't automate away the parts that help people understand their own system.

### Real-world interaction
Some of the best friction is physical or offline — scanning a printed code, a hardware button, a step that asks the person to do something in the world before continuing. Use this sparingly and with purpose.

## Example: confirm with consequences (TypeScript)

```ts
type DestructiveAction = {
  verb: string;              // "Delete"
  target: string;            // "workspace 'Notes'"
  consequences: string[];    // concrete, countable effects
  reversible: boolean;
  confirmPhrase?: string;    // require typing for high-stakes cases
};

const deleteWorkspace: DestructiveAction = {
  verb: "Delete",
  target: "workspace 'Notes'",
  consequences: ["214 notes", "12 shared links will stop working", "3 collaborators lose access"],
  reversible: false,
  confirmPhrase: "Notes",
};
```

Render the consequences as a list; enable the button only when the phrase matches. Contrast with a reversible action: skip the dialog, act immediately, and show a 10-second **Undo** toast.

## Example: AI as proposal, not action

```ts
type Proposal<T> = { summary: string; diff: T; accept: () => Promise<void>; reject: () => void };

// Instead of: await ai.reorganizeNotes();
const proposal = await ai.proposeReorganization(notes);
showPreview(proposal); // person reviews moves/renames, accepts all, some, or none
```

## Decision guide

1. **Is the action reversible?** → Prefer undo over confirm.
2. **Is it high-stakes or irreversible?** → Show consequences; require deliberate input.
3. **Does it affect autonomy (privacy, money, attention, data)?** → Explicit choice, no sneaky default.
4. **Is it AI-initiated?** → Proposal first; auto-action only when explicitly delegated and reversible.
5. **Is the effort pure waste?** → Remove it.

## When reviewing a design

List every point of effort in the flow and classify it as *waste*, *useful*, or *missing* (a place where a pause or choice should exist but doesn't). Recommend removing waste first — that builds the trust that makes useful friction feel respectful rather than annoying.
