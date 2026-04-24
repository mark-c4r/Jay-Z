---
ticket: jarda#reshape-2026-04-23
status: active
appetite: S
risk_score: 1
project: jarda-ai-start
updated: 2026-04-24
parent: docs/plans/prds/2026-04-24-reshape/slice-2-blueprint.md
files:
  - index.html
  - styles/shared.css
---

# Slice 3 — `shared.css` extraction

## Problem

The current `index.html` inlines ~1438 lines of CSS (L14–L1451) inside a `<style>` block. Slice 2 D12 locked the token inventory and the extraction order; Slices 4 (main-page rewrite) and 5 (research pages) both need a shared stylesheet to link. Extracting is a mechanical prerequisite — no design decisions, no voice calls.

## Verified Assumptions

VA rows describe POST-BUILD state per same-session-ship LEARNED pattern (2026-04-19) — the table documents what's true in the shipped code, which is what future /ship re-runs should validate.

| Claim | Source | Status | Verified At | Verify |
|-------|--------|--------|-------------|--------|
| `styles/shared.css` exists and contains the extracted CSS including `.research-*` selectors | [styles/shared.css](styles/shared.css) | VERIFIED | 2026-04-24T11:00:00-05:00 | test -s styles/shared.css && rg -q "\.research-" styles/shared.css |
| `index.html` links `styles/shared.css` and no longer carries an inline `<style>` HTML tag | [index.html](index.html) | VERIFIED | 2026-04-24T11:00:00-05:00 | rg -q 'href="styles/shared.css"' index.html && ! rg -q '^\s*<style>\s*$' index.html |
| Slice 2 D12 extraction policy (token inventory + extraction order + `.research-*` preservation) remains authoritative reference | [docs/plans/prds/2026-04-24-reshape/slice-2-blueprint.md:356](docs/plans/prds/2026-04-24-reshape/slice-2-blueprint.md) | VERIFIED | 2026-04-24T11:00:00-05:00 | rg -q "^### D12 " docs/plans/prds/2026-04-24-reshape/slice-2-blueprint.md && rg -q "shared.css extraction plan" docs/plans/prds/2026-04-24-reshape/slice-2-blueprint.md |

## Shape Decision

Move `<style>` content verbatim to `styles/shared.css`. Replace the `<style>…</style>` block in `index.html` with a single `<link rel="stylesheet" href="styles/shared.css">`. Zero refactor during the move — token restructuring, dossier-class additions, and `:root` reorganization are explicitly deferred to Slice 4/5 follow-up work. This is a move, not a rewrite.

## Acceptance Criteria

- [x] `styles/shared.css` exists, is non-empty, contains the verbatim CSS from `index.html` L14–L1451 (1438 lines extracted)
- [x] `index.html` has no `<style>` / `</style>` HTML tags remaining (the string "style" appears only inside a JS comment at line ~1099 referencing the old block — not an actual tag)
- [x] `index.html` links `styles/shared.css` at the same line position the `<style>` block occupied (after Google Fonts link, L13)
- [x] `index.html` line count dropped by 1439 (from 2827 → 1388)
- [x] `styles/shared.css` preserves `.research-*` selectors verbatim (D12 existing-selector preservation policy)
- [x] Brace balance in `styles/shared.css` is even (367 open / 367 close — no truncation)
- [x] Red-flag grep on this PRD (blockquote-scoped `^> `) returns zero denylist matches (no drafted copy in this PRD, so vacuously clean)

## Slices

### Slice 3 — single sub-slice (THIS DOCUMENT) [downhill]

**Demo.** `ls jarda-ai-start/styles/shared.css` shows a non-empty file; `rg -q "<style>" jarda-ai-start/index.html` returns non-zero; `rg -q 'href="styles/shared.css"' jarda-ai-start/index.html` returns zero exit.
**Files.** `index.html`, `styles/shared.css`
**Steps.**
1. Create `styles/` directory.
2. Extract L14–L1451 to `styles/shared.css` via `sed -n '14,1451p'`.
3. Replace L13–L1452 in `index.html` with `  <link rel="stylesheet" href="styles/shared.css">` via a Python in-place rewrite (BSD sed `c\` across 1440 lines is unreliable).
4. Verify: line-count delta, `<style>` tags absent, `<link>` tag present, shared.css preserves `.research-*` selectors.
5. Commit.

**Tests.** Verification Commands section below.
**Depends on.** Slice 2 (approved + committed 2026-04-24).

## No-Gos

- **No CSS refactoring.** No token renaming, no `:root` reorganization, no dossier-class additions in this slice. That's Slice 4/5 work.
- **No HTML changes beyond the `<style>` → `<link>` swap.** Class names, IDs, structure all untouched.
- **No pixel-diff automation.** Browser-based screenshot comparison isn't available in this session; structural grep + line-count delta is the acceptance proxy.
- **No Codex review.** Risk = 1; below MANDATORY threshold (risk ≥ 4) per `rules/shape-up.md` §Cross-Model Review.

## Verification Commands

Run from `/Users/profile_1/Coding/jarda/jarda-ai-start/`:

1. `test -s styles/shared.css` — shared.css exists and is non-empty
2. `! rg -q "<style>" index.html` — no `<style>` tag remains
3. `rg -q 'href="styles/shared.css"' index.html` — link tag present
4. `test "$(wc -l < index.html | tr -d ' ')" -lt 1500` — index.html shrank to <1500 lines
5. `rg -q "\.research-" styles/shared.css` — `.research-*` selectors preserved per D12
6. `bash ~/Coding/Agentic_Workflow_Setup/scripts/preflight-aggregator.sh docs/plans/prds/2026-04-24-reshape/slice-3-css-extraction.md` — exits 0
