---
ticket: jarda-ai-start/cluster-4-design-ia
status: superseded
superseded-by: 2026-04-21-round-2-master.md
appetite: M
risk_score: 5
project: jarda-ai-start
updated: 2026-04-21
files:
  - jarda/jarda-ai-start/index.html
---

# Cluster 4 — Design / IA refactor (v2b remediation)

**Target file (on apply, outside plan mode):** `/Users/profile_1/Coding/jarda/jarda-ai-start/docs/plans/2026-04-21-cluster-4-design-ia.md`

## Problem

Four tightly-related design concerns surfaced by friend review + Gemini adversarial review of v2a:

1. **(a) Desktop breathing** — the page opens with text at ~y=60px (stop meta + H1 directly under topbar). No masthead, no arrival beat. Feels cramped on desktop; reader does not register "this is a course" before they're in Stop 1.
2. **(b) No top-of-page overview** — reader lands inside Stop 1 with no clickable survey of what's ahead. Lilys.ai-style TOC is absent. The rail is present but cognitively thin as an overview because it's left-margin ambient chrome, not a first-contact affordance.
3. **(c) Redundant stop-nav** — six `.stop-nav` blocks appear after each stop, duplicating the sticky bottom-nav and the rail. Friend: "this bar after every stop seems unnecessary". Three redundant surfaces carry the same job (prev/next/jump).
4. **(d) "Block N of M" vocabulary** — unexplained to reader. Friend: "what are blocks? they're in each stop?". Inconsistent casing (capital B in Stop 1 stop-meta + topbar, lowercase in Stops 2–6 block-label/try-one-label). Appears in `.stop-meta`, `.block-label`, `.try-one-label`, and `.topbar-block` — four surface classes.

## Verified Assumptions

| Claim | Verify command | Ground truth (2026-04-21) |
|---|---|---|
| Exactly 6 `.stop-nav` blocks exist | `grep -c 'class="stop-nav"' jarda/jarda-ai-start/index.html` | 6 |
| `.block-label` divs appear 8 times (Stops 2–6 diagram+reading) | `grep -c 'class="block-label"' jarda/jarda-ai-start/index.html` | 8 |
| `.try-one-label` divs appear 6 times (one per stop) | `grep -c 'class="try-one-label"' jarda/jarda-ai-start/index.html` | 6 |
| Topbar lives at line 1282–1287, contains hamburger + stop indicator + progress + block counter | `sed -n '1282,1287p' jarda/jarda-ai-start/index.html` | confirmed — structure matches |
| Topbar `.topbar-block` carries "Block N of M" via `#tb-block` / `#tb-blocks-total` | `grep -n 'topbar-block\|tb-block\|tb-blocks-total' jarda/jarda-ai-start/index.html` | line 1053 (CSS) + line 1286 (DOM) |
| Hamburger `#menu-toggle` hidden on ≥900px, shown <900px | `sed -n '1045,1060p' jarda/jarda-ai-start/index.html` | confirmed — `display: none` default, flex at <900 breakpoint |
| Casing inconsistency: Stop 1 uses "Block 1 of 3" (capital B); Stops 2–6 block-label use "block 2 of 3" (lowercase b) | `grep -n 'Block \|block ' jarda/jarda-ai-start/index.html \| head -30` | Stop 1 line 1306 `Block 1 of 3`; Stop 2 line 1416 `block 2 of 3` — confirmed drift |
| Stop 1 stop-meta includes "Block 1 of 3"; Stops 2–6 stop-meta only includes "Block 1" (no total) | `grep -n 'stop-meta">Stop' jarda/jarda-ai-start/index.html` | lines 1306, 1380, 1454, 1527, 1605, 1708 — Stop 1 is the outlier |
| Bottom-nav exists at bottom of layout (sticky on <900px) | `grep -n 'class="bottom-nav"' jarda/jarda-ai-start/index.html` | confirmed (CSS at 1078–1086) |
| Rail exists as `<aside id="rail">` at line 1290 | `grep -n 'id="rail"' jarda/jarda-ai-start/index.html` | confirmed — line 1290 |

Every claim above was grep-confirmed against working-tree `index.html` during shaping (2026-04-21T14:xx local). Re-verify before build — single-session ship pattern, same-day mtime expected.

## Shape Decision

**Recommend bundle: A1 + B1 + C1 + D1.** Lowest-risk combination that addresses all four friend concerns. Mirrors Gemini's ranking (#1 Monospace Masthead, #2 Kill hamburger — the latter earned by B1's presence).

| Concern | Chosen | Rejected / Deferred |
|---|---|---|
| (a) Desktop breathing | **A1 — Monospace masthead** (1px border top+bottom, `Claude Cowork: Jay-Z Edition` left, `6 stops · ~12 min` right, mono font, ~10 CSS lines) | A2 gray hero (too blocky, introduces imagery conversation we don't want); A3 tabbed-ledger (too functional, doesn't solve "page arrival" feel) |
| (b) Top-of-page overview | **B1 — Horizontal progress string** (`1. Start here — 2. Your first project — 3. Memory — 4. Connectors + safety — 5. Real work — 6. Your first week` as clickable `<a href="#stop-N">` anchors, below masthead, above Stop 1) | B2 card grid (doubles LOC, introduces SVG thumbnail scope); B3 collapsible-TOC-as-hero (biggest structural refactor — defer) |
| (c) Stop-nav redundancy | **C1 — Delete all 6 `.stop-nav` blocks** (rail + sticky bottom-nav + new top TOC all serve the nav job; three surfaces ≥ four) | C2 (keep one at page-end — deferred; if reader-testing shows a need for "back to top" we add one row under Research, not under Stop 6); C3 (smaller up/next pair — still redundant with bottom-nav) |
| (d) "Block" vocabulary | **D1 — Remove "Block N of M" entirely** from `.block-label`, `.try-one-label`, `.stop-meta`, and `.topbar-block` | D2 rename to "part" (still a jargon problem, 30+ replaces); D3 glossary line (adds copy to explain chrome — wrong direction) |

**Hamburger decision (spillover from Cluster 2 Bug #4):** with B1 + A1 shipped, the top TOC replaces the drawer's role for <900px users. **RECOMMEND killing the hamburger** in an optional Slice 4, but only if Slices 1–3 land inside appetite. The hamburger's CSS/JS (lines 1045–1065, 1971) is removable cleanly because the drawer is opt-in; deletion doesn't orphan content.

**Cross-cluster dependencies:**
- Cluster 2 Bug #1 (top-bar scroll-sync): not a blocker. Masthead sits above an unchanged topbar; scroll-sync can land independently.
- Cluster 3 Stop 0 / Setup: if Setup ships as Stop 0, B1 progress string becomes 7 items (`0. Setup — 1. Start here — …`). Coordinate when Cluster 3 merges; until then, ship 6 items.
- Cluster 5 YouTube chapters: irrelevant to this cluster. Label shape changes anyway if chapters render.

## Acceptance Criteria

- [ ] Desktop top-of-page shows a monospace masthead, ≥120px tall, containing the course title and `6 stops · ~12 min` meta, above the existing topbar
- [ ] Top-of-page contains a visible horizontal progress string linking all 6 stops (7 if Cluster 3 lands first); anchors resolve to `#stop-1` … `#stop-6`
- [ ] Zero `.stop-nav` elements remain: `grep -c 'class="stop-nav"' index.html` returns `0`
- [ ] Zero "Block N of M" strings remain in `.block-label`, `.try-one-label`, `.stop-meta`, `.topbar-block`: `grep -iE '(class="(block-label\|try-one-label\|stop-meta\|topbar-block)")[^<]*</?[^>]*>[^<]*[Bb]lock' index.html` returns `0` (or equivalent audit)
- [ ] Topbar still shows stop + progress; "Block" text is removed from `#tb-block` / `#tb-blocks-total` zone (retire `.topbar-block` OR repurpose to show stop title / percent — pick one, document in commit)
- [ ] Privacy audit exits 0 (`scripts/privacy-audit.sh` or equivalent; no new external asset URLs introduced by masthead)
- [ ] Voice grep clean (no `{your region}` / `{notable credential}` / `🚀` / marketing-copy patterns); run `grep -iE '\{(your |notable )[a-z]+\}|🚀|unlock|supercharge' index.html` — expected 0
- [ ] Lighthouse a11y ≥ 0.95 post-refactor (anchors have visible focus ring, masthead not announced as a heading that competes with Stop 1 H1 — use `<header role="banner">` or plain `<div>` with non-heading content)
- [ ] Chrome MCP visual verification: screenshot at 1440×900 shows masthead + progress string visible above fold; screenshot at 375×812 shows progress string wraps or becomes scrollable without horizontal page overflow
- [ ] No orphaned CSS: `.stop-nav`, `.sn-prev`, `.sn-next` style rules (lines 1169–1171) deleted together with DOM
- [ ] `.block-label` and `.try-one-label` CSS classes remain (labels still needed: "Diagram", "Try one", "Short reading") — only the " · block N of M" suffix is stripped; verify label text still reads as intended

## Slices

### Slice 1 — Masthead + top TOC (~70 LOC)
Downhill 🔽. Pure additive HTML + CSS, no JS.
- Add `<header class="page-masthead">` above existing `<header class="topbar">`
- CSS: monospace stack (`ui-monospace, SFMono-Regular, …`), 1px solid top+bottom, `padding: 28px 32px`, grid two-column (title left, meta right), collapses to single column <640px
- Add `<nav class="page-toc" aria-label="Jump to stop">` with `<ol>` of 6 anchor links (use short titles from existing `#stop-N` H1s: "Start here", "Your first project", "Memory", "Connectors + safety", "Real work", "Your first week")
- Verify: render at 1440×900 + 375×812, confirm no layout shift in existing stops

### Slice 2 — Remove 6 `.stop-nav` blocks (~40 LOC delete)
Downhill 🔽. Pure deletion, semantic-safe.
- Delete the six `<nav class="stop-nav">` blocks at lines 1371–1378, 1445–1452, 1519–1526, 1597–1604, 1700–1707, 1778–1785 (line ranges will shift after Slice 1 — re-grep at build time)
- Delete orphaned CSS rules `.stop-nav`, `.stop-nav .sn-next`, `.stop-nav a:hover` (lines 1169–1171)
- Coordinates with Cluster 2 Bug #8: if that ticket also plans to touch bottom-nav per-stop update, confirm we're not stepping on each other. Ship this slice first or in same commit.
- Verify: `grep -c 'stop-nav' index.html` returns 0; bottom-nav still updates correctly per stop (manual scroll test + rail still has full list)

### Slice 3 — Strip "Block N of M" vocabulary (~18 text edits)
Downhill 🔽. Mechanical search-replace across 4 surface classes.
- Stop meta (6 occurrences, lines 1306, 1380, 1454, 1527, 1605, 1708): change `Stop N of 6 · Block X of Y` → `Stop N of 6` (drop the block clause entirely)
- `.block-label` (8 occurrences): change `Diagram · Block 2 of 3` / `Short reading · block 3 of 4` → `Diagram` / `Short reading` (strip the middot + suffix)
- `.try-one-label` (6 occurrences): change `Try one · block N of M` → `Try one`
- `.topbar-block` (line 1286): delete the element OR repurpose to show `·   {current stop title}` (the latter is lower-risk — DOM shape preserved for scroll-sync script). Decision at build time; favor "delete the element, simplify grid to 3 columns" unless JS has a handle.
- Retire `#tb-block` + `#tb-blocks-total` IDs if element deleted; audit JS at line 1971+ for references (grep first, delete broken selectors second)
- Verify: `grep -iE 'block [0-9]' index.html` returns 0 (may need to exclude drawer copy that talks about "block" in prose — none exist per current grep, but confirm)

### Slice 4 (OPTIONAL) — Kill the hamburger (~30 LOC delete)
Only if Slices 1–3 land ≤3hr.
- Delete `#menu-toggle` button (line 1283), its CSS (lines 1045–1049, 1059), and its JS handler at line 1971+
- Replace the `☰` affordance with a `[N/6]` compact stop indicator on <900px (uses existing `#tb-stop` span — repurpose, don't duplicate)
- The rail becomes click-the-progress-string on mobile (B1 anchors already work) — verify still accessible without drawer
- If this slice is skipped: Cluster 2 Bug #2 (hamburger focus/behavior) is fixed there. No harm in deferring.

## Rabbit Holes

- **Tempting visual-signature pass** (gradient, custom webfont, icon set): NO. Out of scope. Sober register stays. The masthead is monospace + 1px rules; nothing else.
- **Tempting "fix the rail while we're here"** (merge rail into top TOC, drop the aside): NO. Rail is working and serves scroll-sync. Merging it is structural — the deferred alternative bundle (A2 + B3 + C2 + D2) already accounts for that refactor; wait.
- **Tempting to also rewrite block-label copy** ("Diagram" → "Visualize" etc.): NO. Slice 3 strips the suffix only. Word choice is not a friend concern.
- **Tempting to "fix" Cluster 2 Bug #1 here** (topbar scroll-sync): NO. That's a different cluster. Ship this cluster assuming topbar scroll-sync may or may not be present.

## No-Gos

- No `{your region}` / `{notable credential}` / `{city}` copy patterns
- No decorative emoji in new masthead or TOC (existing nav glyphs `▸ ○ → ← ✓` inside the body are fine and unchanged)
- No logo / brand mark / favicon work
- No marketing copy in the masthead ("Learn AI in 12 minutes!" → no). Title + stop count + time estimate only.
- No new external assets (images, fonts from CDN). Masthead font is system monospace stack. No network impact.
- No JS framework pull-in. Vanilla HTML + CSS; topbar scroll-sync JS is untouched.
- No changes to `<title>`, `<meta>` tags, or OG tags in this cluster.

## Verification Commands

```
# Run from jarda/jarda-ai-start/
grep -c 'class="stop-nav"' index.html                    # expect 0
grep -c 'class="page-masthead"' index.html               # expect 1
grep -c 'class="page-toc"' index.html                    # expect 1
grep -iE 'block [0-9]' index.html                        # expect 0 (excluding JS)
grep -c 'class="block-label"' index.html                 # expect 8 (unchanged class; only text stripped)
grep -c 'class="try-one-label"' index.html               # expect 6 (unchanged class; only text stripped)
grep -iE '\{(your |notable )[a-z]+\}|🚀|unlock|supercharge' index.html  # expect 0
# Privacy audit (adapt to project script if named differently)
bash scripts/privacy-audit.sh || true
# Visual: run Chrome MCP screenshot at 1440x900 and 375x812, eyeball masthead + TOC above fold
```

## Challenger Questions (preempts)

**Q1: Does the top TOC duplicate the rail on desktop?**
> A: Yes, partially — both link to the 6 stops. Intentional: the rail is ambient chrome scanned during scroll; the top TOC is an on-arrival affordance scanned at page-load. Two jobs, two surfaces. If user testing shows the redundancy is friction (not signal), collapse by dropping the rail on ≥900px — but that's a later ticket, not this one.

**Q2: Does killing all 6 `.stop-nav` strand mobile users past the bottom-nav tap target?**
> A: No. The sticky bottom-nav persists (CSS line 1084: `@media (max-width: 899px) { .bottom-nav { position: sticky; bottom: 0; ... } }`), so prev/next is always one tap away on mobile. The rail-drawer (`☰` until Slice 4) gives mobile users a full list. Slice 4 only ships if Slice 1's top TOC proves navigable on mobile — we verify that at 375×812 before touching the drawer.

**Q3: Is "Block N of M" load-bearing for any other logic?**
> A: Possibly. `#tb-block` + `#tb-blocks-total` are IDs — the scroll-sync JS at line 1971+ probably updates them. Slice 3's build step: `grep -n 'tb-block\|tb-blocks-total\|topbar-block' index.html` BEFORE deletion. If JS sets them on scroll, we have two choices: (a) delete the IDs and remove matching JS (simpler), (b) keep the element as a hidden stub so JS still has a target (safer). Favor (a); fall back to (b) if a test fails.

**Q4: Does the monospace masthead clash with the sober register?**
> A: Monospace is sober — it's what README.md files look like. It reads as "manual / spec / plain-text" rather than "design". Gemini's ranking anticipates this: A1 was picked over A2 (gray hero, which starts to feel like a marketing page) precisely because monospace holds register.

**Q5: Is A1 + B1 enough to signal "this is a course" on desktop, or do we need a diagram?**
> A: Gemini + friend reviewed for "breathing + arrival", not "diagram". B1's progress string is a lightweight diagram (7 labeled nodes in a horizontal chain). If post-ship feedback says "I still don't get what this is", the fix is Cluster 3's Setup/Stop 0 ("what you need before you start") — that's where a diagram earns its keep, not the masthead.

## Risk Score (5/8 rationale)

- Novelty: 1 (HTML+CSS only, no new patterns)
- Reversibility: 1 (pure diff, `git revert` restores)
- Dependencies: 1 (cross-cluster coordination with Cluster 2 Bug #8 + Cluster 3 Stop 0)
- Interface uncertainty: 2 (Gemini vs friend vs Lilys.ai reference — three opinions converge on A1+B1+C1+D1 but not identically)
- **Total: 5.** Medium risk. Full flow (Clarify → Explore → Contract) already done in this shaping doc; adversarial review MANDATORY per workflow (risk ≥4).

## Adversarial Review Hook

Per `~/.claude/rules/shape-up.md` cross-model review policy: risk ≥ 4 → MANDATORY. Before ExitPlanMode approval, invoke `codex-challenger` on this contract. Expected P1 blockers to watch for:
- `#tb-block` JS handle safety (Q3 above — may surface as Blocker)
- Progress-string overflow at 375px (Q2 adjacent)
- Whether Slice 4 hamburger kill introduces an orphan a11y path

Round cap: 2. Round 3 only if round 2 surfaces a named directional contradiction (e.g., "kill topbar entirely" vs "keep topbar, delete only masthead").
