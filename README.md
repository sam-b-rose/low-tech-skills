# Low-Tech Skills

A small set of [Claude skills](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview) for designing calmer, more humane software. They borrow the legible, finite shapes of early-2000s technology (loading bars, save points, menus, a computer that lived in one room) and apply them to modern products and AI systems.

## Inspiration

These skills are based on the talk **[The future is low-tech: lessons from the early 2000s](https://www.youtube.com/watch?v=otkSbl399tU)** by Jésabel DC at [Figma Config 2026](https://config.figma.com/san-francisco/session/79c76468-0c48-41ae-8775-7a46d4409bb3/).

The talk covers calm, nervous-system-friendly design: attention regulation, slowness as a feature, autonomy-first mechanics, real-world interaction, and gentle feedback loops. The skills are organized around the four ideas in Jésabel DC's *The Future Is Low-Tech* framework: **Orientation**, **Useful Friction**, **Boundaries**, and **Letting the User Go**.

This is an independent interpretation of those ideas, not an official resource from the speaker or Figma. Watch the talk for the original argument.

## The skills

| Skill | What it does | Use it for |
|---|---|---|
| [`low-tech-design-review`](./skills/low-tech-design-review/SKILL.md) | The hub. Reviews a flow against all four principles, scores each from 0 to 3, and proposes fixes in tiers. | Design critiques, product audits, "make this calmer" |
| [`orientation-design`](./skills/orientation-design/SKILL.md) | Helps people know *where they are, what's happening, how long it will take, and what comes next.* | Loading states, AI/agent status, multi-step flows, save/sync state |
| [`useful-friction`](./skills/useful-friction/SKILL.md) | Separates wasteful effort from effort that builds understanding, agency, and safety. | Confirmations, defaults, AI auto-actions, destructive or purchase flows |
| [`boundaries-and-exits`](./skills/boundaries-and-exits/SKILL.md) | Designs clear beginnings, endings, and easy exits, and success metrics that don't rely on time spent in the app. | Feeds, notifications, streaks, cancel flows, retention strategy |

The hub skill points to the other three, so they work as one review process. Each skill includes short TypeScript patterns, such as staged progress for AI tasks, a typed save state, confirm-with-consequences, and a notification urgency classifier.

## Examples

Try these after installing:

- "Review our onboarding flow for calm, low-tech principles: welcome → 5 permission prompts → suggested-accounts feed."
- "Our agent tasks take 30s–4min and we show a spinner. Design a better status UI."
- "Should 'Delete workspace' be one click? Admins want it faster."
- "Redesign our infinite feed so people reach a clear 'you're caught up' moment."
- "Sort our notifications into interrupt now / batch / remove."

## Installation

### Claude Code (plugin)

Install all four skills as a plugin from inside a session (Claude Code 2.1.275 or later):

```
/plugin install low-tech-skills --marketplace sam-b-rose/low-tech-skills
```

Or from your shell:

```bash
claude plugin marketplace add sam-b-rose/low-tech-skills
claude plugin install low-tech-skills@sam-b-rose
```

Get updates with `claude plugin update low-tech-skills@sam-b-rose`. Plugin skills are namespaced, so they appear as `/low-tech-skills:low-tech-design-review` and so on.

### Any agent (`npx skills`)

Install with Vercel's [skills CLI](https://github.com/vercel-labs/skills), which works with Claude Code, Cursor, Codex, and other agents:

```bash
npx skills add sam-b-rose/low-tech-skills          # pick skills and agents interactively
npx skills add sam-b-rose/low-tech-skills -g       # install globally
npx skills add sam-b-rose/low-tech-skills --skill useful-friction -a claude-code
```

### Claude apps (claude.ai, desktop, mobile)

Download a skill's `.zip` from the [latest release](https://github.com/sam-b-rose/low-tech-skills/releases/latest) and upload it as a custom skill.

### Manual

Copy any folder from [`skills/`](./skills) into `~/.claude/skills/` (personal) or `.claude/skills/` (project).

## Contributing

These are a starting point. Try them on real flows, see where the rubric or patterns feel off, and refine. Issues and PRs are welcome.

## License

[MIT](./LICENSE). The skills are an independent interpretation of the talk; the talk itself belongs to its speaker and Figma.
