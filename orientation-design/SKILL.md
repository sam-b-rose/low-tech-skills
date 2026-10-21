---
name: orientation-design
description: Design interfaces that help people know where they are, what the system is doing, and what comes next — honest progress indicators, visible system state, menus and maps instead of feeds, clear instructions, and gentle feedback loops. Use whenever the user is building loading states, progress bars, multi-step flows, onboarding, navigation, AI/agent status displays, sync or save indicators, empty states, or any UI where "what's happening right now?" could be unclear.
---

# Orientation Design

Older software was explicit about itself. Loading bars showed how far along you were. Installers listed each step. Games had a pause menu and a map. Manuals told you what buttons did. People rarely wondered *where am I?* or *is it doing anything?*

Modern products often hide state in the name of seamlessness — and AI systems make this worse, because so much happens invisibly. Orientation design restores legibility: **the person should always be able to answer four questions.**

1. **Where am I?** (location in the product / flow)
2. **What is happening?** (system state right now)
3. **How long / how much is left?** (progress and expectation)
4. **What can I do next?** (available actions, including leaving)

## Patterns

### Honest progress
- Prefer **determinate** progress (steps, %, item counts) over indeterminate spinners whenever the work is measurable.
- When it isn't measurable, show **stages** ("Reading files → Planning → Writing → Checking") instead of a single spinner.
- Never fake progress (bars that race to 90% then stall). If estimates are uncertain, say so.

### Visible system state
- Make invisible states visible: saved / unsaved, syncing / offline, queued / running / done, AI drafting / waiting for you.
- For agents and automations, keep a **readable activity log** — what it did, when, and how to undo.

### Maps over feeds
- Give a structure people can hold in their head: menus, tabs, numbered steps, a table of contents.
- Feeds are fine for browsing, but the main tasks should be reachable from a stable map, not surfaced by an algorithm.

### Instructions in context
- Short, plain explanations near the control, shown once and easy to recall — like a game's tutorial level.
- Name things consistently. A label used in the UI should match the label in docs and notifications.

### Gentle feedback loops
- Feedback should **inform, not escalate**: a calm confirmation ("Saved · 2 min ago") rather than celebration or alarm for routine events.
- Reserve stronger signals (color, motion, sound) for things that genuinely need attention.
- Close the loop: every action the person takes should have a visible, proportional response.

## Example: staged progress for an AI task (TypeScript)

```ts
type Stage = { id: string; label: string };
type Status = "pending" | "active" | "done" | "error";

const stages: Stage[] = [
  { id: "read",  label: "Reading your notes" },
  { id: "group", label: "Clustering by theme" },
  { id: "draft", label: "Drafting summaries" },
  { id: "check", label: "Checking links" },
];

function renderStages(current: string, failed?: string) {
  const idx = stages.findIndex(s => s.id === current);
  return stages.map((s, i) => {
    const status: Status =
      s.id === failed ? "error" : i < idx ? "done" : i === idx ? "active" : "pending";
    return { ...s, status, step: `${i + 1} of ${stages.length}` };
  });
}
```

Pair this with a plain-language line under the active stage ("Found 42 notes, grouping into ~6 themes") — specifics orient far better than a generic "Working on it…".

## Example: visible save state

```ts
type SaveState =
  | { kind: "saved"; at: Date }
  | { kind: "saving" }
  | { kind: "unsaved"; changes: number }
  | { kind: "offline"; queued: number };

const label = (s: SaveState) => {
  switch (s.kind) {
    case "saved":   return `Saved · ${timeAgo(s.at)}`;
    case "saving":  return "Saving…";
    case "unsaved": return `${s.changes} unsaved change${s.changes === 1 ? "" : "s"}`;
    case "offline": return `Offline · ${s.queued} change${s.queued === 1 ? "" : "s"} will sync`;
  }
};
```

A discriminated union forces every state to have a visible label — a small structural nudge toward orientation.

## Checklist

- [ ] Every async operation longer than ~1s has a progress or stage indicator
- [ ] Long or uncertain operations show stages with specific, human copy
- [ ] Save / sync / connection state is always visible in editing contexts
- [ ] Agents and automations expose a log and an undo path
- [ ] Primary tasks are reachable from a stable menu or map, not only a feed
- [ ] Each step in a multi-step flow shows "step N of M" and allows going back
- [ ] Routine confirmations are quiet; strong signals are reserved for real issues
- [ ] Empty states explain what will appear and how to get started

## When reviewing a design

Walk the flow and, at each screen, answer the four questions from the person's point of view. Any "I'm not sure" is an orientation gap — propose the smallest visible cue that resolves it.
