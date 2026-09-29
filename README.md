# scannable-ui

An agent skill that makes AI-built interfaces feel *weirdly perfect* — by making them fast to scan.

Nobody reads a screen; people hunt for one answer. This skill gives your coding agent six concrete layout rules (plus a few proven fundamentals) to apply while building UI, and a checklist to audit existing UI.

## Install

```bash
npx skills add geetansh/scannable-ui
```

Global install for Claude Code only:

```bash
npx skills add geetansh/scannable-ui -a claude-code -g
```

## The six rules

1. **Lock every element to edges** — hard-left content, hard-right values; manufacture edges (dividers, sub-lines) instead of adding filler or hiding actions.
2. **Constrain the width** — keep text at 45–75 characters per line and keep rows from stretching across wide screens.
3. **Differentiate before you add whitespace** — group by what people search for and vary element types; density is fine, sameness isn't.
4. **Show, don't tell** — avatars, icons, chips, and diagrams over labels and tooltips (but never ambiguous icon-only buttons).
5. **Emphasis is relative** — defaults gray, changes colored, one accent per view.
6. **Dissolve unnecessary cards** — no borders on borders or stacked radii; column edges and section headings do the work.

## What's inside

| File | Purpose |
| --- | --- |
| `SKILL.md` | The rules, build workflow, and when to bend them |
| `references/patterns.md` | Before/after code: profile card, task list, settings panel, dashboard |
| `references/audit-checklist.md` | Pass/fail checklist and report format for reviewing UI |

## Credit

Inspired by the video [The secret behind weirdly perfect UI designs](https://www.youtube.com/watch?v=neE6wOuBIP8). Rules are paraphrased and extended; code examples are original.

## License

MIT
