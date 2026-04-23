---
ticket: jarda-ai-start/cluster-2-bug-sweep
status: superseded
superseded-by: 2026-04-21-round-2-master.md
appetite: M
risk_score: 4
project: jarda-ai-start
updated: 2026-04-21
files:
  - index.html
---

# Cluster 2 — Bug sweep (v2b live)

## Problem

v2b is live. Friend-feedback + mobile/desktop testing surfaced **7 real bugs + 2 bonuses**, clustering into three failure modes:

1. **Scroll/state desync** — top-bar + bottom-nav hard-coded; never update as the reader scrolls. User feels stuck on Stop 1, perceives "only Jeff Su on mobile" (really: Stop 1 top-bar never advanced).
2. **Mobile navigation breakage** — rail drawer click navigates but viewport stays put (scrollIntoView while fixed drawer overlays viewport — mobile Safari/Chrome aborts). `sn-jump → #rail` silently no-ops on mobile because rail is `display:none` outside `.rail-open`.
3. **Video seek fidelity** — highlight click activates facade but ignores `data-seek`, so "click 2:15" opens the video at 0:30 (`facade.dataset.start`).

Cumulatively this reads as "broken product" to a first-time visitor, even though the content is intact.

**Demand-side test:** "Can a mobile reader (a) see which stop they're on, (b) jump to a specific stop, (c) click a timestamp and land at that second of the video?" Today: no / mobile-broken / no. After: yes across the board.

## Verified Assumptions

| # | Claim | Verify | Status |
|---|---|---|---|
| 1 | No IntersectionObserver or scroll-driven `state.currentStop` update exists. Only `onStopClick` at line 1929 mutates currentStop. | `rg -n "IntersectionObserver\|scroll.*currentStop" index.html` → zero hits outside `state.currentStop` reads/writes at lines 1905/1911/1932/1941/1947 | ✅ verified 2026-04-21 |
| 2 | Rail `display: none` on mobile until `.rail-open`. Drawer is fixed-position, 85vw, z-index 40 (line 1061-1062). | `rg -n "\.rail\s\{\|rail-open" index.html` lines 1060-1062 | ✅ verified |
| 3 | Delegated rail listener fires `setTimeout(closeDrawer, 100)` AFTER `onStopClick` already called `scrollToStop`. Lines 2034-2040. | `rg -n "setTimeout\(closeDrawer" index.html` → line 2038 | ✅ verified |
| 4 | 6 in-stop `.stop-nav` blocks (Stops 1-6) each contain `.sn-jump href="#rail"`. Lines 1371/1445/1519/1597/1700/1778. | `rg -c "class=\"sn-jump\"" index.html` → 6 | ✅ verified |
| 5 | `activateFacade(facade)` at line 2057 destructures `start` from `facade.dataset` only — no parameter override. Caller at line 2078 has `a.dataset.seek` available but doesn't pass it. | Read lines 2057-2068 + 2071-2084 | ✅ verified |
| 6 | `.bottom-nav` CSS: `font-size: 12px; padding: 13px 22px` (lines 1078-1082). Anchors are bare `<a>` with no explicit min-height. | Read lines 1078-1086 + 1837-1841 | ✅ verified |
| 7 | Bottom-nav markup hard-codes `href="#stop-2"` for next, `aria-disabled="true"` for prev. Never mutated by JS. Lines 1838-1840. | `rg -n "bottom-nav\|bn-prev\|bn-next" index.html` → only line 1974 reads it (`.hidden` toggle for drawer); never rewrites hrefs | ✅ verified |
| 8 | 6 sections `<section id="stop-N" class="stop">` exist. `.stop` padding = 28px top (line 1089) — intersection thresholds need a small offset to fire near viewport top. | `rg -n 'id="stop-' index.html` → 6 hits at 1304/1378/1452/stop-4/stop-5/stop-6 | ✅ verified |
| 9 | `.highlights-hint` text is static HTML in 12 highlight blocks (stops 1-6, some multi-block). Currently always reads "click to jump". | `rg -n "highlights-hint" index.html` → 12 hits | ✅ verified |

## Shape Decision

**Ship bugs 1-8 in one sweep. Defer bug 9 to Cluster 4.**

- **Bug 6 is fixed-by-proxy via Bug 1** (the "only Jeff Su on mobile" perception is really "top-bar shows Stop 1 forever"). Do NOT dispatch a dedicated fix; verify in AC instead.
- **Bug 4 option (b) — delete the 6 in-stop stop-nav blocks** — wins over option (a). Simpler, friend-corroborated, and removes the failure mode entirely rather than working around it. Deletion also removes the "Previous stop / Next stop / Jump to any" redundancy with the footer bottom-nav.
- **Bug 7 label swap is optional.** Include it — the text cost is trivial and it keeps the hint honest. Swap happens when facade activates.
- **Bug 9 (Block N of M capital/lowercase + prefix inconsistency) defers to Cluster 4** (design/IA refactor that may rename or eliminate "block" entirely). Touching it now risks two passes.

### Why M, not L

Risk score 4 = Low-medium (1-2 new patterns via IntersectionObserver + activateFacade signature change; fully reversible; single file; well-understood interfaces). Three small slices, each independently verifiable. Scope is clearly bounded. The diff is additive JS + surgical HTML deletion + CSS media-query tweak.

### Why not S

Touches 3 surfaces (JS state, HTML markup, CSS media queries), affects navigation semantics, and needs mobile-device verification. One approval checkpoint between slices is warranted.

## Acceptance Criteria

- [ ] **Bug 1 — Top-bar scroll sync.** As reader scrolls past stop section boundaries, `.tb-stop` (top-bar) + rail-current marker + bottom-nav prev/next update to reflect the stop currently at the top of the viewport. Verify via `preview_eval`: scroll to `document.querySelector('#stop-4').offsetTop + 10`, read `document.getElementById('tb-stop').textContent` → "4".
- [ ] **Bug 2 — Mobile hamburger rail click.** Open drawer via menu-toggle. Click "Stop 3" rail entry. Expected: drawer closes FIRST, then viewport scrolls to `#stop-3`. Verify in mobile viewport (375×812): after click, `document.querySelector('.rail.rail-open')` is null AND `window.scrollY` is within 100px of `#stop-3` top.
- [ ] **Bug 3 — Footer tap target.** On `max-width: 899px`, `.bottom-nav a` computed `height` ≥ 44px. Verify: `preview_inspect('.bn-next', ['height', 'min-height', 'font-size'])` → height ≥ 44, font-size ≥ 15px.
- [ ] **Bug 4 — In-stop stop-nav removed.** Zero `.sn-jump` elements remain. Verify: `rg -c "class=\"sn-jump\"" index.html` → 0.
- [ ] **Bug 5 — Highlight click respects data-seek.** On Stop 1, click highlight with `data-seek="135"`. Iframe src contains `&start=135`, not `&start=0` or `&start=<facade.dataset.start>`. Verify via `preview_eval` reading `grid.querySelector('iframe').src`.
- [ ] **Bug 6 — Perception resolved.** Bug 1 fix removes the "only Jeff Su" perception. Verify: scroll through page on mobile viewport; confirm all 6 stops' top-bar label changes + bottom-nav next/prev updates.
- [ ] **Bug 7 — Hint text updates post-facade (optional).** Before facade click: hint reads "· click to start here". After: "· click to jump". Skip if adds >10 min; ship bug 5 without.
- [ ] **Bug 8 — Bottom-nav sync.** Same observer as Bug 1 also rewrites `.bn-prev href`, `.bn-next href`, `.bn-prev aria-disabled`, `.bn-next aria-disabled` based on current stop. On Stop 1: prev disabled. On Stop 6: next disabled. Verify: `preview_eval` at each stop boundary.
- [ ] **Privacy audit exit 0** — `python3 scripts/privacy-audit.py` (existing script) passes.
- [ ] **Lighthouse a11y ≥ 0.95** on mobile + desktop.
- [ ] **No regressions to Cluster 1 scope** — yt-facade activation, drawer open/close, and rail render still work.

## Slices

### Slice A — JS: scroll sync + seek override + bottom-nav reorder

**~80-100 LOC in the IIFE at line 1846. No HTML changes. No CSS changes.**

1. **IntersectionObserver for current-stop tracking.** After `renderRail()` wiring, add:
   - `const stopSections = document.querySelectorAll('section.stop[id^="stop-"]');`
   - Observer with `rootMargin: '0px 0px -85% 0px'` so intersection fires when a section's top nears viewport top.
   - `threshold: 0`
   - On intersect: `state.currentStop = parseInt(entry.target.id.replace('stop-', ''), 10);` → `renderRail()` + `updateTopbar()` + new `updateBottomNav()`.
   - Throttle via `requestAnimationFrame` guard to avoid thrash.
   - Rail `aria-live` announcement remains throttled (same guard).
2. **New `updateBottomNav()` helper.** Reads `state.currentStop`, writes:
   - `.bn-prev`: if stop === 1, `href="#"` + `aria-disabled="true"`; else `href="#stop-${n-1}"` + no aria-disabled.
   - `.bn-next`: if stop === 6, `href="#"` + `aria-disabled="true"`; else `href="#stop-${n+1}"` + no aria-disabled.
   - `.bn-jump`: opens drawer on mobile (wire through existing `openDrawer()` if viewport < 900).
3. **Reorder drawer close + scroll in `onStopClick` (line 1929).** Inside handler:
   - `if (drawerOpen) closeDrawer();`
   - `requestAnimationFrame(() => scrollToStop(stop));`
   - Remove the 100ms `setTimeout(closeDrawer, 100)` at line 2038 (delegated listener). Keep the delegated listener itself as a safety net for edge cases but have it be a no-op when `onStopClick` already closed the drawer.
4. **`activateFacade(facade, startOverride)` signature change at line 2057.**
   - Inside: `const startValue = startOverride ?? start;`
   - Build iframe src with `startValue`. Drop `end` when `startOverride` is set (seeking past a bounded clip is nonsensical).
   - Caller at line 2078: `activateFacade(facade, a.dataset.seek);`
5. **(Optional, bug 7) Label swap.** On facade click, also do `facade.closest('.block-grid')?.querySelector('.highlights-hint').textContent = '· click to jump';` (facade-activated → post-play). Pre-facade initial text to `'· click to start here'` in the HTML. Skip if out of appetite.

**Demo:** open in mobile viewport. Scroll. Top-bar counts up. Click rail on mobile — drawer closes, viewport scrolls. Click timestamp — opens at that second.

**Depends on:** nothing (Cluster 1 scaffolding already shipped).

**Files:** `index.html` (JS block only).

**Tests:** preview_eval-driven AC checks 1, 2, 5, 8.

### Slice B — CSS: mobile tap-target fix

**~5-8 LOC change to existing `@media (max-width: 899px)` block near line 1083.**

1. Extend the existing `.bottom-nav` mobile block:
   ```css
   @media (max-width: 899px) {
     .bottom-nav {
       position: sticky; bottom: 0; z-index: 20;
       font-size: 15px;
       min-height: 52px;
       padding: 8px 16px;
     }
     .bottom-nav a {
       min-height: 44px;
       display: inline-flex;
       align-items: center;
     }
   }
   ```
2. Verify desktop (>899px) remains unchanged — existing `.bottom-nav` block at line 1078 stays.

**Demo:** preview_inspect at 375px viewport shows height ≥ 44px.

**Depends on:** nothing.

**Files:** `index.html` (CSS block only).

**Tests:** preview_inspect AC check 3.

### Slice C — HTML: remove 6 in-stop stop-nav blocks

**Surgical HTML deletion. No JS touched, no CSS touched (keep `.stop-nav`/`.sn-jump` selectors; just no markup uses them).**

1. Delete 6 `<nav class="stop-nav">…</nav>` blocks at approximately:
   - Stop 1: line 1371-~1376
   - Stop 2: line 1445-~1450
   - Stop 3: line 1519-~1524
   - Stop 4: line 1597-~1602
   - Stop 5: line 1700-~1705
   - Stop 6: line 1778-~1783
   (Exact ranges confirmed at build time via `rg -n "stop-nav\|sn-jump" index.html`.)
2. Leave `.stop-nav` CSS rule at line 1169 intact (trivial cost; removing touches both CSS and HTML and invites merge conflict with any parallel design work).

**Demo:** scroll through each stop — no mid-stop "Previous / Jump / Next" chrome.

**Depends on:** Slice A (bottom-nav now handles prev/next responsibility). Ship A first; if scroll-sync is broken, bottom-nav is the only prev/next affordance.

**Files:** `index.html` (HTML body only).

**Tests:**
- `rg -c "class=\"sn-jump\"" index.html` → 0 (AC bug 4)
- `rg -c "class=\"stop-nav\"" index.html` → 0
- Visual: screenshot each stop; confirm no gap/empty-chrome where stop-nav used to sit.

## No-Gos

- **No state module rewrite.** `freshState()`, `loadState()`, `saveState()`, `SCHEMA_VERSION=4` — all untouched.
- **No schema bump.** IntersectionObserver writes `state.currentStop` through the existing write path; no new fields.
- **No content edits.** No rewording of stop titles, rationales, highlights, or research-block text.
- **No rail structural changes.** Drawer markup + open/close remain. Only the timing of close-vs-scroll in `onStopClick` changes.
- **No bug 9 fix.** "Block N of M" casing + prefix inconsistency defers to Cluster 4.
- **No new dependencies.** Vanilla JS, no polyfills (IntersectionObserver has 97%+ support).
- **No facade redesign.** `activateFacade` gets a second optional param; everything else stays.

## Verification Commands

Run all from `/Users/profile_1/Coding/jarda/jarda-ai-start/`.

```bash
# Bug 4: zero sn-jump / stop-nav markup
rg -c 'class="sn-jump"' index.html   # expect 0
rg -c 'class="stop-nav"' index.html  # expect 0

# Bug 5: activateFacade accepts override
rg -n 'function activateFacade' index.html  # signature includes startOverride
rg -n 'activateFacade\(facade, a\.dataset\.seek\)' index.html  # caller passes seek

# Bug 1 + 8: observer wired
rg -n 'IntersectionObserver' index.html  # expect at least 1 hit
rg -n 'updateBottomNav' index.html       # expect function def + invocation

# Bug 2: 100ms setTimeout removed
rg -n 'setTimeout\(closeDrawer' index.html  # expect 0

# Bug 3: mobile tap-target CSS
rg -n 'min-height: 44px' index.html  # expect at least 1 hit inside @media (max-width: 899px)

# Privacy + a11y
python3 scripts/privacy-audit.py  # exit 0
# Lighthouse run via /browse or manually: mobile + desktop ≥ 0.95 a11y

# Interactive smoke
# preview_start jarda-local
# preview_eval: scroll to each stop → document.getElementById('tb-stop').textContent
# preview_eval at 375×812: open drawer, click rail entry, confirm scroll
# preview_eval: click highlight with data-seek → iframe src includes &start=<seek>
```

## Rollback

Each slice is a single commit. Revert in reverse order: Slice C (1 commit, restore 6 nav blocks) → Slice B (1 commit, CSS) → Slice A (1 commit, JS). Non-destructive throughout — feature flag not needed at this scale.

## Post-ship

1. Screenshot each stop on mobile (375×812) + desktop (1400×900). Commit to `docs/verification/2026-04-21-cluster-2-bugs/`.
2. Log to `LEARNED.md` if any of the 8 bugs surfaces a pattern worth capturing (expected: "hard-coded nav state + scroll-driven content = desync every time" may warrant an entry).
3. Feed bug 9 into Cluster 4's intake.
