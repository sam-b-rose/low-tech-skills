# Low-Tech Skills

A small set of [Claude skills](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview) for designing calmer, more humane software. They borrow the legible, finite shapes of early-2000s technology (loading bars, save points, menus, a computer that lived in one room) and apply them to modern products and AI systems.

## Inspiration

These skills are based on the talk **[The future is low-tech: lessons from the early 2000s](https://www.youtube.com/watch?v=otkSbl399tU)** by Jésabel DC at [Figma Config 2026](https://config.figma.com/san-francisco/session/79c76468-0c48-41ae-8775-7a46d4409bb3/).

The talk covers calm, nervous-system-friendly design: attention regulation, slowness as a feature, autonomy-first mechanics, real-world interaction, and gentle feedback loops. The skills are organized around the four ideas in Jésabel DC's *The Future Is Low-Tech* framework: **Orientation**, **Useful Friction**, **Boundaries**, and **Letting the User Go**.

This is an independent interpretation of those ideas, not an official resource from the speaker or Figma. Watch the talk for the original argument.

## The skills

| Skill | What it does | Use it for |
|---|---|---|
| [`low-tech-design-review`](./low-tech-design-review/SKILL.md) | The hub. Reviews a flow against all four principles, scores each from 0 to 3, and proposes fixes in tiers. | Design critiques, product audits, "make this calmer" |
| [`orientation-design`](./orientation-design/SKILL.md) | Helps people know *where they are, what's happening, how long it will take, and what comes next.* | Loading states, AI/agent status, multi-step flows, save/sync state |
| [`useful-friction`](./useful-friction/SKILL.md) | Separates wasteful effort from effort that builds understanding, agency, and safety. | Confirmations, defaults, AI auto-actions, destructive or purchase flows |
| [`boundaries-and-exits`](./boundaries-and-exits/SKILL.md) | Designs clear beginnings, endings, and easy exits, and success metrics that don't rely on time spent in the app. | Feeds, notifications, streaks, cancel flows, retention strategy |

The hub skill points to the other three, so they work as one review process. Each skill includes short TypeScript patterns, such as staged progress for AI tasks, a typed save state, confirm-with-consequences, and a notification urgency classifier.

## Installation

Each skill is a folder containing a `SKILL.md`. To use one:

- **Claude apps:** zip the skill folder and upload it as a custom skill.
- **Claude Code:** copy the folder into `~/.claude/skills/` (personal) or `.claude/skills/` (project).

```bash
# Package every skill as a zip
for d in */; do [ -f "$d/SKILL.md" ] && zip -qr "${d%/}.zip" "$d"; done
```

## Contributing

These are a starting point. Try them on real flows, see where the rubric or patterns feel off, and refine. Issues and PRs are welcome.
