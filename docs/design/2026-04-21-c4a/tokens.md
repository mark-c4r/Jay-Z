# C4a tokens + CSS-to-implementation table

**Cluster:** C4a (structural — masthead, save-page, diagram-label)
**Shape doc:** `docs/plans/2026-04-21-round-2-master.md` §4a
**Built against:** `index.html` @ `d5b291d` (Day 1 ship)
**Gate artifact:** this file + 3 mockup SVGs in `docs/design/2026-04-21-c4a/`

## Design-token usage

**No new CSS tokens introduced.** All C4a additions reuse the existing closed set declared at `index.html` `:root`:

| Token | Role in C4a | Example use |
|---|---|---|
| `var(--bg)` | Topbar background (unchanged) | existing `.topbar` |
| `var(--ink)` | Primary text color | byline chip text |
| `var(--muted)` | De-emphasized text color | duration badge text, byline chip (recommended) |
| `var(--accent)` | Affordance color for save-page button | `.save-page-button` border + text |
| `var(--rule)` | Vertical separator line | `.topbar-duration` left border |
| `var(--rule-soft)` | (unchanged, used by completion-reveal) | — |
| `var(--focus-ring)` | Button focus state (inherited from global) | `.save-page-button:focus-visible` |

## Selectors + properties

### C4a.1 — Topbar enrichment

**Existing `.topbar` grid** (`index.html:1040-1044`):
```css
.topbar {
  position: sticky; top: 0; z-index: 20;
  display: grid; grid-template-columns: auto 1fr auto auto; gap: 16px; align-items: center;
  padding: 10px 22px; background: var(--bg); border-bottom: 1px solid var(--rule);
}
```

**Change:** expand grid from 4 columns to 6 columns.

```css
.topbar {
  /* menu-toggle | byline | stop-counter | progress | block | duration */
  grid-template-columns: auto auto 1fr auto auto auto;
}
```

**New selectors:**

```css
.topbar-byline {
  font-size: 12px;
  color: var(--muted);
  font-weight: 500;
  white-space: nowrap;
}
.topbar-duration {
  font-size: 11px;
  color: var(--muted);
  padding-left: 12px;
  border-left: 1px solid var(--rule);
  white-space: nowrap;
}

/* < 900px — hamburger visible, hide duration, compress byline */
@media (max-width: 899px) {
  .topbar {
    grid-template-columns: auto auto 1fr auto auto;
  }
  .topbar-duration {
    display: none;
  }
  .topbar-byline {
    /* keep visible but shorten via content swap in HTML; OR keep as-is */
    font-size: 11px;
  }
}
```

**HTML edit (at `index.html:1282-1287`):**

```html
<header class="topbar" role="banner">
  <button id="menu-toggle" aria-label="Open course menu" aria-expanded="false" aria-controls="rail">☰</button>
  <div class="topbar-byline">A primer by Mark</div>                                           <!-- NEW -->
  <div class="topbar-stop">Stop <span id="tb-stop">1</span> of 6 · <span id="tb-title">Start here</span></div>
  <div class="topbar-progress" aria-hidden="true"><div class="topbar-progress-fill" id="tb-fill"></div></div>
  <div class="topbar-block" aria-live="polite">Block <span id="tb-block">1</span> of <span id="tb-blocks-total">3</span></div>
  <div class="topbar-duration">~20 min</div>                                                  <!-- NEW -->
</header>
```

**AC:**
- No topbar height increase on desktop (padding 10px stays; font-size ≤12px keeps chip within line-height)
- Byline chip visible at all breakpoints
- Duration badge hidden <900px
- No new tokens
- Accessibility: both new elements are plain `<div>` text — no new ARIA needed

### C4a.2 — Save-page button

**New selector:**

```css
.save-page-button {
  display: inline-block;
  margin-top: 20px;
  padding: 8px 18px;
  font-family: inherit;
  font-size: 13px;
  font-weight: 600;
  color: var(--accent);
  background: transparent;
  border: 2px solid var(--accent);
  border-radius: 4px;
  cursor: pointer;
  transition: background 120ms ease-out;
}
.save-page-button:hover,
.save-page-button:focus-visible {
  background: color-mix(in oklab, var(--accent) 8%, transparent);
}
```

**HTML edit — append to `#completion-reveal` after second `.completion-copy` paragraph (around `index.html:1791`):**

```html
<button type="button" class="save-page-button" onclick="window.print()">Save this page</button>
```

### C4a.2 — Print-state fix (Decision §3 option A)

Append inside the existing `@media print { ... }` block ending at `index.html:1034`, OR add a new `@media print` block after the completion-reveal CSS around `index.html:1276`.

**Recommended: new `@media print` block immediately after `.completion-copy` (line 1276):**

```css
@media print {
  /* C4a.2 — ensure completion-reveal prints even if reader hits Save before finishing */
  .completion-reveal[hidden] { display: block !important; }
  /* Hide the save button itself in print (no one needs a button in a PDF) */
  .save-page-button { display: none !important; }
}
```

**Why a second `@media print` block instead of extending the existing one at 946:** the existing block targets v1 tabpanel/tab-nav classes that don't exist in v2b — it's a historical print stylesheet for a layout that's been removed. Extending it mixes unrelated concerns. A dedicated C4a `@media print` block is block-local and easier to reason about per the Codex R2 convergent P1 (block-local AC > whole-file changes).

**AC:**
- Reader can print the full primer after clicking Save (completion-reveal included even if `hidden`)
- Save button itself doesn't print
- No JS beyond the single `window.print()` call

### C4a.3 — Stop 1 diagram label

**File edit:** `assets/diagrams/stop-1-positioning.svg`

Changes per `diagram-label.svg` mockup:
1. `viewBox` height: `260` → `300`
2. Y-shift all existing elements (boxes at y=60-165, axis at y=210) by +40: boxes to y=100-205, axis to y=250-268
3. New label text `"For developers"` at x=534, y=42, styled with existing `.label` class (font-size 14 → use 12 for subtlety)
4. New bracket path spanning x=366→702 at y=52, with 6px downticks on each end (x=366,x=702; y=52→58)
5. Add `<desc>` text mentioning the new label

**`<img alt>` update (at `index.html:1343`):**

Current alt text (inferred — confirm at build):
`"Positioning: ChatGPT, Cowork, Code, and Codex — four boxes in a row showing where each tool fits on a spectrum from simpler/conversational to more autonomous/technical."`

New alt text (appended clause):
`"...more autonomous/technical. A small 'For developers' label sits above the Code and Codex columns."`

**AC:**
- `grep -c "For developers" assets/diagrams/stop-1-positioning.svg` → 1
- `<img alt>` mentions "For developers"
- SVG ≤ 50KB (current is small, the change adds ~200 bytes)
- Visual style matches existing: 2px strokes, `#222` ink, Inter font — no aesthetic drift

## Print-state AC summary (all of C4a.2)

- `rg -n "Save this page" index.html` → 1
- `rg -n "window\.print" index.html` → 1
- `rg -n 'completion-reveal\[hidden\]' index.html` → 1
- `rg -c "save-page-button" index.html` → ≥ 2 (CSS selector + HTML class attr, may be more with print rule)

## What this doc locks

- Design tokens: closed set, none added (matches C4a AC §4a line 447 + master-shape §1 invariants)
- Byline copy: exactly `"A primer by Mark"` (masthead) — C3 prereq card will have a longer variant; byline-split Decision §1 of plan keeps both
- Duration copy: exactly `"~20 min"`
- Save-page button copy: exactly `"Save this page"`
- Stop 1 diagram label copy: exactly `"For developers"` (no punctuation, no variant like "For developers only")
- Print-state strategy: option A (`@media print` override on `[hidden]`), no UX friction copy, no JS

## What this doc explicitly does NOT cover

- The operator visually approving the SVG mockups — that's Phase 1 checkpoint, not a doc
- Lighthouse a11y run — operator runs manually in Chrome devtools post-deploy (handover Part 7 notes no automated command)
- C3 prereq-card byline slot copy — lives in C3 master-shape section §3.a, not here
- Stop 1 diagram `excalidraw-source/` refinement pass — style-guide §"v2a placeholder SVGs" notes these are placeholders for later Excalidraw refinement; C4a.3 edit stays at placeholder-SVG fidelity
