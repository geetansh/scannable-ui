---
name: scannable-ui
description: Layout rules that make interfaces fast to scan — edge alignment, line length, differentiation over whitespace, visuals over labels, relative emphasis, and de-carding. Use when building, reviewing, or fixing any UI component or screen (cards, lists, task lists, tables, settings panels, sidebars, dashboards, chat inputs, kanban boards), when a layout feels cluttered, crowded, empty, unbalanced, or "off", when asked to make a UI cleaner, more polished, or more professional, or when a design has nested cards, too many borders, too many colored badges, or walls of text.
---

# Scannable UI

Nobody reads a screen. People arrive with one question and hunt for the answer — one file, one setting, one task. Every rule below exists to make that hunt faster. None of them are about making things prettier; the polish is a side effect of scannability.

Apply these while building (build mode) or when reviewing an existing UI (audit mode — see Workflow).

---

## 1. Lock every element to edges

**Rule:** Every element should sit against at least two edges — a container edge, or the edge created by the element stacked above/beside it.

**Why:** Edges are what the eye tracks. A receipt has no dividers and almost no whitespace, yet it reads instantly because labels run hard left and prices run hard right. Two strong edges hold everything together.

- **Do** align text hard left and values/actions hard right (`flex justify-between`, `grid-cols-[1fr_auto]`).
- **Do** center only what isn't meant to be read (IDs, barcodes, decorative marks, empty states).
- **Do** use every edge a card gives you: 4 container edges, plus the bottom edge of a header row (avatar + name) that the next row can stack onto.
- **Do** manufacture a new edge when content floats: a divider, a header strip, or a sub-line under a large icon/avatar so the row regains a bottom edge.
- **Don't** fill empty space by adding more content — it looks padded.
- **Don't** fix a crowded row by hiding secondary actions in a `…` menu. First cut actions, then reposition the rest onto edges.
- **Don't** center body text or labels inside compact UI (cards, lists, forms).

## 2. Constrain the width

**Rule:** Lines of text and rows of content must not run the full width of a wide screen.

**Why:** Even with every edge in place, full-width rows force long eye travel between the left label and the right value, and long lines of text are tiring to read. Readable measure is 45–75 characters.

- **Do** cap text blocks at `max-width: 65ch` (`max-w-prose`), and cap list/settings columns (`max-w-2xl`/`max-w-3xl`) with `mx-auto` or a sidebar layout.
- **Do** keep label→value distance short enough that the pair still reads as one row.
- **Don't** let `w-full` rows stretch across a 1440px+ viewport.

## 3. Differentiate before you add whitespace

**Rule:** Density is fine. *Undifferentiated* density is the problem. Group and vary content before reaching for padding.

**Why:** Extra spacing helps a little but makes everything longer. Grouping and varied element types let the eye jump straight to the right chunk, regardless of how much content there is (proximity and common region — Gestalt).

- **Do** group by the dimension people search by (due date, status, owner, category) with small section headers.
- **Do** vary element types: avatars where people are referenced, chips for categories, icons for types, monospace for IDs, tables for comparable data.
- **Do** keep spacing inside a group tighter than spacing between groups.
- **Don't** respond to a wall of rows by only increasing `gap`/`py`.
- **Don't** render every row with identical weight, size, and color.

## 4. Show, don't tell

**Rule:** Replace text with visuals people recognize instantly — avatars, icons, chips, status dots, mini diagrams, blue underlined links.

**Why:** Recognition beats reading. A red octagon means "stop" with no words. When something is unclear, the instinct is to explain harder (add a label, a comparison, a tooltip); each addition is technically more information but makes the screen harder to read.

- **Do** turn repeated plain-text attributes into icons/chips/diagrams (e.g. a progress bar instead of "7 of 10 complete", an avatar stack instead of a names list).
- **Do** make interactive values look interactive: links blue + underlined, tags as chips that can be clicked to change.
- **Do** keep text labels where the icon is not universal. An action bar of ambiguous icon-only buttons that needs tooltips to decode is *worse* than text. Position can carry meaning (a select-all checkbox above a list), but only when it's conventional.
- **Don't** add tooltips, helper text, or legends as the first fix for confusion — fix the visual first.

## 5. Emphasis is relative

**Rule:** An element stands out only by being different from its neighbors. Emphasis is not a property of the element; it's the contrast with its surroundings (isolation / von Restorff effect).

**Why:** A checkbox is a thin border when off and earns fill + checkmark when on — color *is* the signal of change. A settings panel where every value chip is colored is like checkboxes that are blue when off: nothing stands out.

- **Do** render default / unchanged / inactive values muted (gray text, outline or ghost chips) and give color only to non-default, changed, or attention-worthy values.
- **Do** reserve the accent color for one thing per view — usually the primary action.
- **Do** create emphasis by quieting the surroundings before boosting the element.
- **Do** keep muted text readable: gray text must still meet WCAG AA (4.5:1 for body, 3:1 for large text/UI).
- **Don't** fix "nothing stands out" by making one element bolder/brighter while everything else is already loud.
- **Don't** give every badge, chip, or icon its own color.

## 6. Dissolve unnecessary cards

**Rule:** Don't structure a page by boxing everything. Cards give you four free edges, but a page full of them ends up with borders on borders and stacked corner radii.

**Why:** A single column line and section headers do the same job the card edges were doing — every row still stacks onto the one above it — with less noise.

- **Do** use one outer container (or none), then `divide-y`, a shared left column edge, and section headings for structure.
- **Do** keep the other rules intact after de-carding: rows stack, sections group, chips/icons carry meaning, defaults stay gray.
- **Don't** nest bordered/shadowed containers (card → panel → card). Max one level of visible container.
- **Don't** stack different border radii (e.g. `rounded-2xl` inside `rounded-xl` inside `rounded-lg`). If nesting is unavoidable, inner radius = outer radius − padding.

---

## Workflow

**Build mode** (creating UI):
1. Decide what question the user brings to this screen. That determines grouping (rule 3) and what deserves emphasis (rule 5).
2. Lay out edges first: left column for labels/content, right column for values/actions (rule 1). Cap width (rule 2).
3. Group and vary content (rule 3), swap text for recognizable visuals (rule 4).
4. Set everything to its quiet default; color only the non-default and the single primary action (rule 5).
5. Remove any container that doesn't earn its border (rule 6).

**Audit mode** (reviewing/fixing UI): walk through `references/audit-checklist.md`. For each failed check, report: location → which rule → concrete fix (code-level when you have the source). Then apply fixes if asked.

For before/after code examples (profile card, task list, settings panel, dashboard), read `references/patterns.md`.

## When to bend the rules

- Marketing heroes, empty states, onboarding, and single-message screens can be centered — they're meant to be read once, not scanned.
- Data-dense pro tools (trading, IDEs, logs) may exceed the 75ch measure for tables; keep label/value alignment strict instead.
- Brand-driven pages may use more color, but still keep one clear primary action per view.
