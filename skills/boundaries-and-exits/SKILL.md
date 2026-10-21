---
name: boundaries-and-exits
description: Design clear beginnings, endings, and easy exits so products help people accomplish something and then let them go — finite sessions, "you're done" states, stopping cues, calm notifications, attention regulation, and success metrics that don't depend on time-on-app. Use whenever the user is designing feeds, sessions, notifications, emails, streaks, gamification, cancel/unsubscribe flows, completion screens, retention strategy, engagement metrics, or asks how to make an app less addictive or more respectful of attention.
---

# Boundaries & Letting the User Go

Older technology had natural edges. You turned the computer on and off. A game cartridge had a save point. A Tamagotchi needed you briefly, then didn't. A website had a last page. These edges gave people **closure** — and closure is what lets someone feel done and go live their life.

Engagement-optimized products remove edges: infinite feeds, autoplay, streaks that punish breaks, notifications engineered to pull people back. This skill restores boundaries and reframes success around **helping people accomplish something without demanding more of their attention than that requires**.

## Three boundaries to design

### 1. Clear beginnings
- The person knows *why* they're here and *what* they can do in this session.
- Entry is intentional: opening the app goes to the person's task, not to a feed designed to divert.

### 2. Clear endings
- Every core flow has a **done state** that feels like closure: summary of what was accomplished, nothing urgently "next".
- Finite containers by default: pages, chapters, daily sets, inbox zero, "you're all caught up".
- After the goal is met, *stop* — no autoplay, no "you might also like" wall.

### 3. Easy exits
- Leaving, pausing, muting, and cancelling are as easy as joining.
- Breaks don't cost the person anything (no lost streaks, no guilt copy). Prefer "pause" or "freeze" over penalties.
- Data export and account deletion are findable and plain.

## Attention regulation

Treat attention as the person's budget, not the product's inventory.

- **Notifications:** default to off for anything non-essential. Prefer batched digests at a time the person picks. Every notification should answer "what does the person need to do, and why now?"
- **Ambient over interruptive:** when something just needs awareness, use a badge, a quiet status line, or a daily summary — not a push.
- **Respect rhythm:** quiet hours by default; no re-engagement pings designed to break someone's break.

## Letting the user go (commercially)

Products can succeed without capturing maximum attention. Metrics and models that align with letting go:

| Instead of… | Consider… |
|---|---|
| Daily active users, time in app | Tasks completed, time-to-done, return-by-choice rate |
| Streaks and loss aversion | Progress the person can see and own |
| Ad-funded attention capture | Subscriptions, one-time purchases, usage-based pricing |
| Re-engagement campaigns | Asking people when they'd like to hear from you |
| Churn prevention mazes | Easy pause + a respectful "come back anytime" |

Frame trade-offs honestly: some engagement metrics may drop, while trust, word-of-mouth, and willingness to pay often rise.

## Pointing back to the real world

Good tools often end by handing the person back to their life: a printable list, a reminder at the right moment then silence, an encouragement to go do the thing. Design some exits to lead *offline*, not to another screen.

## Example: a finite session with closure (TypeScript)

```ts
type Session = {
  goal: string;            // set by the person at the start
  items: string[];         // finite set for this session
  completed: string[];
};

function nextStep(s: Session) {
  if (s.completed.length === s.items.length) {
    return {
      kind: "done" as const,
      summary: `You finished ${s.completed.length} items toward "${s.goal}".`,
      actions: ["Close", "Plan next session"], // no infinite "more"
    };
  }
  return { kind: "continue" as const, item: s.items[s.completed.length] };
}
```

## Example: calm notification policy

```ts
type Urgency = "now" | "digest" | "never";

function classify(event: { userInitiated: boolean; blocksUser: boolean; timeSensitive: boolean }): Urgency {
  if (event.blocksUser && event.timeSensitive) return "now"; // e.g. 2FA, failed payment
  if (event.userInitiated) return "digest";                   // replies, results they asked for
  return "never";                                             // re-engagement, "we miss you"
}
```

Default every user to digest at a time they choose; let them opt up, not down.

## Checklist

- [ ] Opening the product lands on the person's task, not a diversion
- [ ] Every core flow has an explicit, satisfying done state
- [ ] Feeds and lists are finite by default or have an "all caught up" boundary
- [ ] No autoplay or auto-continue after a goal is met
- [ ] Non-essential notifications are off or batched by default
- [ ] Taking a break has no penalty; pause is offered alongside cancel
- [ ] Cancel / unsubscribe / delete take no more steps than sign-up
- [ ] Success metrics include task completion, not just time spent

## When reviewing a design

Trace one realistic session from open to close. Mark where it begins, where the person's goal is met, and where the product *actually* lets them stop. The gap between "goal met" and "allowed to stop" is the boundary problem — propose ways to close it.
