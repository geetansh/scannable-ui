# Scannable UI — Before / After Patterns

Examples use HTML + Tailwind. The ideas translate directly to any stack; plain-CSS equivalents are noted where helpful.

---

## 1. Profile card — manufacture an edge, cut the buttons

**Before:** content floats, five buttons wrap in the middle, nothing lines up.

```html
<div class="rounded-xl border p-6 text-center">
  <img class="mx-auto h-16 w-16 rounded-full" src="avatar.jpg" />
  <h3 class="mt-3 font-semibold">Maya Chen</h3>
  <p class="text-sm text-gray-500">Product Designer</p>
  <div class="mt-4 flex flex-wrap justify-center gap-2">
    <button class="btn">Message</button><button class="btn">Follow</button>
    <button class="btn">Share</button><button class="btn">Invite</button>
    <button class="btn">Report</button>
  </div>
</div>
```

Problems: centered text in a compact card (rule 1), buttons don't touch any edge (rule 1), too many equally loud actions (rule 5).

**After:** a header row creates a new bottom edge; avatar, name and actions share it; rare actions are removed rather than hidden.

```html
<div class="w-80 rounded-xl border">
  <div class="flex items-center gap-3 border-b p-4">          <!-- manufactured edge -->
    <img class="h-10 w-10 rounded-full" src="avatar.jpg" />
    <div class="min-w-0 flex-1">
      <h3 class="truncate font-semibold">Maya Chen</h3>
      <p class="truncate text-sm text-gray-500">Product Designer</p>
    </div>
    <button class="rounded-md bg-blue-600 px-3 py-1.5 text-sm text-white">Message</button>
  </div>
  <dl class="divide-y text-sm">
    <div class="flex justify-between px-4 py-2"><dt class="text-gray-500">Team</dt><dd>Design Systems</dd></div>
    <div class="flex justify-between px-4 py-2"><dt class="text-gray-500">Location</dt><dd>Berlin</dd></div>
  </dl>
</div>
```

Every element now touches ≥2 edges: left/right container edges plus the header's bottom edge or the row divider above it. One accent action.

---

## 2. Task list — differentiate instead of padding

**Before:** 12 identical rows; the only fix tried is `py-4`.

```html
<ul class="space-y-4">
  <li>Review onboarding copy — assigned to Sam — due Mon — Design</li>
  <li>Fix login redirect — assigned to Priya — due Tue — Bug</li>
  <!-- … -->
</ul>
```

**After:** grouped by due date (what people search by), people as avatars, categories as chips, due info in the right column.

```html
<section class="max-w-2xl">
  <h4 class="px-2 pb-1 pt-4 text-xs font-medium uppercase tracking-wide text-gray-500">Today</h4>
  <ul class="divide-y">
    <li class="grid grid-cols-[auto_1fr_auto] items-center gap-3 px-2 py-2">
      <input type="checkbox" class="h-4 w-4" />
      <span class="truncate">Review onboarding copy <span class="ml-2 rounded-full bg-gray-100 px-2 py-0.5 text-xs text-gray-600">Design</span></span>
      <img class="h-6 w-6 rounded-full" src="sam.jpg" alt="Sam" />
    </li>
    <!-- … -->
  </ul>
  <h4 class="px-2 pb-1 pt-4 text-xs font-medium uppercase tracking-wide text-gray-500">Tomorrow</h4>
  <!-- … -->
</section>
```

Notes: tight spacing inside groups, larger gap between groups. Each line is an edge for the next. Width capped. If rows use large icons instead of checkboxes, add a sub-line (meta text) so the row keeps a bottom edge.

---

## 3. Settings panel — gray defaults, color the changes

**Before:** every value is a colored chip, so nothing stands out.

```html
<div class="flex justify-between"><span>Theme</span><span class="chip bg-blue-100 text-blue-700">System</span></div>
<div class="flex justify-between"><span>Notifications</span><span class="chip bg-blue-100 text-blue-700">All</span></div>
<div class="flex justify-between"><span>Auto-save</span><span class="chip bg-blue-100 text-blue-700">Off</span></div>
```

**After:** defaults are muted outline chips; only the non-default value gets color.

```html
<dl class="max-w-xl divide-y">
  <div class="flex items-center justify-between py-3">
    <dt>Theme</dt>
    <dd class="rounded-full border px-2.5 py-0.5 text-sm text-gray-500">☾ System</dd>        <!-- default -->
  </div>
  <div class="flex items-center justify-between py-3">
    <dt>Notifications</dt>
    <dd class="rounded-full border px-2.5 py-0.5 text-sm text-gray-500">🔔 All</dd>          <!-- default -->
  </div>
  <div class="flex items-center justify-between py-3">
    <dt>Auto-save</dt>
    <dd class="rounded-full bg-amber-100 px-2.5 py-0.5 text-sm text-amber-800">⏸ Off</dd>  <!-- changed -->
  </div>
</dl>
```

Rule of thumb: color means "this differs from normal". Make sure `text-gray-500` on your background still passes 4.5:1 (on white, `#6b7280` passes; lighter grays often don't).

---

## 4. Dashboard — dissolve the cards

**Before:** borders on borders, three radii stacked.

```html
<div class="rounded-2xl border p-6 shadow">
  <div class="rounded-xl border p-4">
    <div class="rounded-lg border p-3">Revenue …</div>
    <div class="rounded-lg border p-3">Users …</div>
  </div>
</div>
```

**After:** one column edge + section headings + dividers do the same work.

```html
<main class="mx-auto max-w-3xl">
  <section>
    <h2 class="border-b pb-2 text-sm font-semibold">Overview</h2>
    <dl class="divide-y">
      <div class="flex justify-between py-3"><dt class="text-gray-500">Revenue</dt><dd class="font-medium tabular-nums">$48,210</dd></div>
      <div class="flex justify-between py-3"><dt class="text-gray-500">Active users</dt><dd class="font-medium tabular-nums">3,904</dd></div>
    </dl>
  </section>
  <section class="mt-8">
    <h2 class="border-b pb-2 text-sm font-semibold">Alerts</h2>
    <!-- … -->
  </section>
</main>
```

Plain CSS equivalents: `divide-y` → `.list > * + * { border-top: 1px solid var(--border) }`; `tabular-nums` → `font-variant-numeric: tabular-nums` (keeps right-aligned numbers on one edge).

If a nested container is unavoidable, match radii: `inner-radius = outer-radius − padding`.
