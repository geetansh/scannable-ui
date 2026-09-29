# Scannable UI — Audit Checklist

Answer each check with pass / fail. For every fail, report: **where** → **rule** → **fix**.

First, write one line: *What question does a user bring to this screen?* Use it to judge grouping and emphasis.

## Edges (rule 1)
- [ ] Every element touches at least two edges (container edge or the edge of a neighboring element).
- [ ] Labels/content align hard left; values, numbers and actions align hard right.
- [ ] Nothing meant to be read is centered inside compact UI (cards, lists, forms, panels).
- [ ] Empty space is resolved with a structural edge (header strip, divider, sub-line), not filler content.
- [ ] Crowded action rows were reduced, not just collapsed into a `…` menu.
- [ ] Rows with large icons/avatars have a sub-line or divider so they keep a bottom edge.

## Width (rule 2)
- [ ] Body text is capped around 45–75 characters per line (`max-width: ~65ch`).
- [ ] List/settings/table rows don't stretch edge-to-edge on wide screens; label and value still read as a pair.

## Differentiation (rule 3)
- [ ] Long lists are grouped by the dimension users search by (date, status, owner, type).
- [ ] Element types vary where meaning varies (avatars for people, chips for tags, icons for types, tables for comparable data).
- [ ] Spacing within a group is tighter than spacing between groups.

## Show, don't tell (rule 4)
- [ ] Repeated plain-text attributes are shown as icons, chips, avatars, or small diagrams where a universal visual exists.
- [ ] Interactive text looks interactive (links blue + underlined; editable tags as chips).
- [ ] No icon-only control depends on a tooltip to be understood.
- [ ] Confusion wasn't "fixed" by stacking extra labels, helper text, or tooltips.

## Emphasis (rule 5)
- [ ] Default / unchanged / inactive values are muted; only non-default or attention-worthy values have color.
- [ ] The accent color is used for at most one primary element per view.
- [ ] Emphasis comes from quiet surroundings, not from an arms race of bold/bright elements.
- [ ] Muted text still meets WCAG AA contrast (4.5:1 body, 3:1 large text and UI components).

## Containers (rule 6)
- [ ] No border/shadow container nested inside another visible container (max one level).
- [ ] No stacked mismatched border radii; nested radii follow `inner = outer − padding`.
- [ ] Structure comes from column edges, dividers, and section headings rather than boxes.

## Report format

```
[fail] Settings › Notifications row — Rule 5 (emphasis)
  All six value chips use bg-blue-100; five are defaults.
  Fix: defaults → `border text-gray-500`; keep color only on "Auto-save: Off".
```

Finish with the top 3 fixes by impact on scan speed.
