---
ticket: jarda#reshape-2026-04-23
status: active
appetite: L
risk_score: 3
project: jarda-ai-start
updated: 2026-04-24
parent: docs/plans/prds/2026-04-24-reshape/slice-2-blueprint.md
files:
  - index.html
  - styles/shared.css
gate_override: auto
gate_override_reason: "styles/ directory is genuinely new territory (created in Slice 3, appended in Slice 4). Novel-path flag is expected and pre-reviewed per D11/D12."
---

# Slice 4 — Main page build (`/index.html`)

## Problem

Slice 2 locked 12 decisions (D1–D12). Slice 3 extracted the inline CSS. The existing `index.html` body still carries the pre-reshape "Stop 1 of 6 · Block 1 of 3" e-learning frame with 24 branch-drawers — the exact chrome C1/C5 identified as the top blocker. Slice 4's job is to replace that body with the new IA per Wireframe A: teaser-forward §1 opening → §2 AI right now → §3 Cowork world → §4 The brief → §5 First-week practice → §6 Deeper research pointers. No voice re-drafting; no re-litigation of Slice 2 decisions.

## Verified Assumptions

VA rows describe POST-BUILD state per same-session-ship LEARNED pattern.

| Claim | Source | Status | Verified At | Verify |
|-------|--------|--------|-------------|--------|
| `index.html` no longer contains `Stop N of 6` or `Block N of 3` e-learning chrome | [index.html](index.html) | VERIFIED | 2026-04-24T12:00:00-05:00 | ! rg -q "Stop [1-6] of 6" index.html && ! rg -q "Block [1-4] of" index.html |
| `index.html` no longer contains `.branch-drawer` entries or `Go deeper` labels (all 24 cut per D10) | [index.html](index.html) | VERIFIED | 2026-04-24T12:00:00-05:00 | ! rg -q 'class="branch-drawer"' index.html && ! rg -q "Go deeper" index.html |
| Opening names the reader in the first addressable line (Jay Z placeholder per README privacy policy) | [index.html](index.html) | VERIFIED | 2026-04-24T12:00:00-05:00 | rg -q "Hi Jay Z" index.html |
| Peer-cluster names appear above the first video embed (teaser-forward per D2) | [index.html](index.html) | VERIFIED | 2026-04-24T12:00:00-05:00 | python3 -c "import re; s=open('index.html').read(); peer_pos=min([s.find(n) for n in ['Ceranna','Avvagraphy','2 Brides','Honest Guide','Paul Zizka'] if s.find(n)>=0]); facade_pos=s.find('yt-facade'); assert peer_pos>=0 and facade_pos>=0 and peer_pos<facade_pos, f'peer {peer_pos} facade {facade_pos}'" |
| All 4 companion videos embedded via `.yt-facade` button pattern preserved from the pre-reshape JS (D12) | [index.html](index.html) | VERIFIED | 2026-04-24T12:00:00-05:00 | test "$(rg -c 'class="yt-facade"' index.html)" = "4" |
| `activateFacade(facade, startOverride)` JS function still present and idempotent (D12 + synthesis D3) | [index.html](index.html) | VERIFIED | 2026-04-24T12:00:00-05:00 | rg -q "function activateFacade" index.html && rg -q "facade.isConnected" index.html |
| Footer copy carries WhatsApp anchor (replacing old "reply to the email" per synthesis hook #7) | [index.html](index.html) | VERIFIED | 2026-04-24T12:00:00-05:00 | rg -q "WhatsApp" index.html && ! rg -q "reply to the email" index.html |
| No real name "Jarda" or "Jarda Zaoral" appears in `index.html` (privacy policy per README.md:5-7) | [index.html](index.html) | VERIFIED | 2026-04-24T12:00:00-05:00 | ! rg -q "Jarda" index.html |

## Shape Decision

Full body rewrite per Wireframe A (D11). Substitute "Jay Z" for "Jarda" in all drafted copy from D5/D7 (privacy policy — blueprint's literal `"Hi Jarda,"` is internal-only). Preserve the `<head>`, `.yt-facade` markup pattern verbatim (D12), and trim the existing JS block to just the facade + chapter-list + timestamp-chip logic (delete Stop/Block state, rail, drawer, and scroll-sync functions — they reference DOM that no longer exists). Add minimal new CSS at the top of `styles/shared.css` for wireframe A's new semantic classes (`.main-brief`, `.letter-body`, `.brief-handoff`, `.companion-text`, `.research-pointers`, `.dossier-humility`, `.progress-line`, `.last-updated`) — enough to render legibly without re-architecting the token system.

**§4 thesis choice (from D8 candidates).** Picking "AI-adjacent service premium" framed through the Ceranna + Paul Zizka lenses — both cited by name per D8 evidence requirement (≥2). Reasoning: it's the thesis where the research vault has concrete observations rather than speculation, and it aligns with the opportunity-scoring that already lives in the peer-cluster research.

**§5 "one habit, one setup, one project" choice.** Shoot-log voice-note habit + bilingual voice-and-style project + inquiry-qualifier skill — the three that appeared in MULTIPLE research documents (trust-family-business-models, codex-R2-C7, opportunity-scoring). Narrower than enumerating all options; deeper than a single vague gesture.

## Acceptance Criteria

- [ ] `<title>` reads "For Jay Z — AI + cowork refresher" (or equivalent "For Jay Z" opening; name-swap honored)
- [ ] `<head>` preserves: charset, viewport, color-scheme, description, robots-noindex, font preconnects, Fraunces+Inter stylesheet link, `styles/shared.css` link
- [ ] §1 Opening carries D5 drafted copy (name-swapped): "Hi Jay Z," ... closes with WhatsApp anchor + —M signoff
- [ ] Peer cluster names (Ceranna · Avvagraphy · 2 Brides · Honest Guide · Paul Zizka) appear inline in §1, above the first video facade
- [ ] §2 AI right now: Jeff Su (z9rdrNrkvDY) + Jack Roberts (cNf7uVff11Y) companions present; each has a `.yt-facade` button + a ~150w memory-trigger summary
- [ ] §3 Cowork world: Jesse Genet ×2 (yiJOTCRVWjc + aFQskhdR3RQ); each has a `.yt-facade` button + a ~290–295w stand-alone summary + 2–3 load-bearing quotes
- [ ] §4 The brief: D7 handoff copy (humility clause A, name-swapped) → 4.1 (~250w, peer cluster evidence) → 4.2 (~200w thesis citing ≥2 peer names) → 4.3 (~250w first move) → 4.4 (~150w where I might be wrong + humility clause B with WhatsApp anchor)
- [ ] §5 First-week practice (~250–350w): one habit, one setup, one project; no drawers — all inline
- [ ] §6 Deeper research: pointer list to 4 sibling `/research/*.html` pages (market-clusters, ten-year-picture, seo-and-discovery, growth-opportunities); one-line rationale each
- [ ] Footer: WhatsApp anchor; no "reply to the email" copy
- [ ] JS block: `activateFacade`, `renderVideoChapters`, facade click/touchend bindings, chapter-button click, timestamp-chip click — present. Stop/Block state, rail, drawer, scroll-sync code — absent.
- [ ] `styles/shared.css` gains appended CSS rules for wireframe A classes at end-of-file (preserving Slice 3 verbatim-move integrity); no rules deleted or re-ordered from Slice 3 extraction
- [ ] Red-flag grep on drafted copy (`^<p\|^<blockquote\|^<h`-ish scoped) returns zero denylist matches: `opinionated|convention|as we say|turns out|the truth is|in our view`
- [ ] Name-leak grep: `rg -q "Jarda" index.html` returns non-zero (no matches = clean)
- [ ] Preflight aggregator on this PRD exits 0 (or documents stable novel-path flag for `styles/shared.css` since it's mutated, not created — which shouldn't flag novel)

## Slices

### Slice 4 — single sub-slice (THIS DOCUMENT) [uphill]

**Demo.** Opening `jarda-ai-start/index.html` in a browser shows a teaser-forward personal brief starting with "Hi Jay Z," the 5 peer-cluster names, four video facades, the §4 brief body, §5 first-week practice, §6 research pointers, and a WhatsApp footer. No Stop/Block chrome. No 24-drawer scaffolding. All facades click-activate.

**Files.** `index.html` (full body rewrite), `styles/shared.css` (append-only new rules for wireframe A classes).

**Steps.**
1. Audit existing JS to isolate keep-set vs drop-set (facade + chapters + highlights-list = KEEP; state/rail/drawer/scroll-sync = DROP).
2. Draft §4 body (4.1 / 4.2 / 4.3 / 4.4) citing research vault; name-swap all occurrences of "Jarda" → "Jay Z" in drafted copy.
3. Draft §5 body with the three "one habit / one setup / one project" choices; name-swap throughout.
4. Write the full new `index.html` with wireframe A structure + drafted copy + preserved `<head>` + trimmed JS.
5. Append wireframe A's new semantic-class CSS rules to `styles/shared.css` (at the end, so Slice 3's verbatim-move block stays grep-identifiable).
6. Run AC checks (VA verify commands + red-flag grep + name-leak grep).
7. Commit.

**Tests.** All Verification Commands below.
**Depends on.** Slices 2 + 3 (both committed).

## Downstream slice dependency map

| Slice | Consumes Slice 4 | Blocked until |
|-------|------------------|---------------|
| Slice 5 — research pages | §6 pointer hrefs define the 4 target paths | Slice 4 committed |
| Slice 6 — proofread pass | Full drafted copy | Slice 4 + 5 committed |

## No-Gos

- **No /research/*.html file creation.** §6 pointer hrefs will 404 until Slice 5 builds those pages. That's acceptable — Slice 5's contract makes them resolve.
- **No re-architecture of shared.css tokens.** Token-system restructure is deferred per D12; Slice 4 only APPENDS new rules for the new semantic classes.
- **No voice re-drafting of the 3 sample pairs** (locked verbatim per Slice 2 No-Gos).
- **No Jarda in index.html.** Privacy policy per README.md:5-7. D5/D7 drafted copy gets name-swapped at this stage.
- **No pre-shaping Slice 5.**
- **No Codex review.** Risk score 3 (below MANDATORY threshold of 4). Build-phase changes are reversible and single-file per-phase.
- **No JS feature additions.** Trim is subtractive only.

## Verification Commands

Run from `/Users/profile_1/Coding/jarda/jarda-ai-start/`:

1. `! rg -q "Stop [1-6] of 6" index.html && ! rg -q "Block [1-4] of" index.html` — Stop/Block chrome removed
2. `! rg -q 'class="branch-drawer"' index.html && ! rg -q "Go deeper" index.html` — drawers removed
3. `! rg -q "Jarda" index.html` — **name leak check** (blocking)
4. `rg -q "Hi Jay Z" index.html` — opening present with correct placeholder
5. `rg -q "Ceranna" index.html && rg -q "Paul Zizka" index.html && rg -q "Avvagraphy" index.html && rg -q "2 Brides" index.html && rg -q "Honest Guide" index.html` — all 5 peer names present
6. `test "$(rg -c 'class="yt-facade"' index.html)" = "4"` — exactly 4 facades
7. `rg -q "function activateFacade" index.html && rg -q "facade.isConnected" index.html` — facade JS preserved
8. `rg -q "WhatsApp" index.html && ! rg -q "reply to the email" index.html` — footer swap
9. `! rg -nE '\b(opinionated|convention|as we say|turns out|the truth is|in our view)\b' index.html` — red-flag grep on main page prose (whole-file scope is OK here since index.html doesn't meta-document the denylist)
10. `bash ~/Coding/Agentic_Workflow_Setup/scripts/preflight-aggregator.sh /Users/profile_1/Coding/jarda/jarda-ai-start/docs/plans/prds/2026-04-24-reshape/slice-4-main-page-build.md` — exits 0
