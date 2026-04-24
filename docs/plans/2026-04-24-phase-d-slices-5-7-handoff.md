---
ticket: jarda#reshape-2026-04-23 (Phase D — Slices 5/6/7)
status: active
project: jarda-ai-start
updated: 2026-04-24
parent: docs/plans/2026-04-23-jarda-reshape-refresher-primer.md
supersedes: docs/plans/2026-04-24-phase-c-slice-2-shaping-handoff.md
---

# Phase D Handoff — Slices 5 / 6 / 7

Fresh-session handoff. Phase C (Slice 2 shaping + approval) and Slices 3 + 4 shipped in the previous session. This doc is self-contained — a new session should NOT need to re-read the Slice 2 blueprint unless it's making a Slice 2 decision change.

## State at handoff

**Shipped this session:**
- `7b838b7` — Slice 2 blueprint (12 decisions locked, Codex R1+R2 folded, preflight PASS)
- `21f4ab5` — Slice 3 CSS extraction (inline `<style>` → `styles/shared.css`, 1438 lines verbatim)
- `db25a77` — Slice 4 main-page build (full `index.html` rewrite per wireframe A, teaser-forward IA)

**NOT shipped (this handoff's scope):**
- Slice 5 — 4 research pages at `/research/*.html` + dossier aesthetic CSS
- Slice 6 — proofread pass (voice + name-leak sweep)
- Slice 7 — ship (git state check / GitHub Pages / Jay Z handoff)

## Critical privacy policy (read this before any edit)

- This repo is PUBLIC at `github.com/mark-c4r/Jay-Z`.
- [README.md:5-7](jarda-ai-start/README.md:5) says: *"The real name, real URLs, and real referral codes never land here. The page uses 'Jay Z' as the reader persona."*
- Internal planning docs leak the real name ("Jarda") — existing state, 5 files public on origin/main before this session; +1 (Slice 2 blueprint) added this session = 6 total after push.
- **Public-facing surfaces (`index.html`, any `/research/*.html`) must be Jarda-clean.** Slice 2 blueprint's drafted copy uses "Jarda"; Slice 4 name-swapped to "Jay Z" at build time. Slice 5 must do the same.
- `docs/plans/` and `docs/research/` are GITIGNORED. Slice-specific PRDs get force-added via `git add -f`. Do NOT bulk-add directories.
- Commit-time guard: `! rg -q "Jarda" index.html` and `! rg -q "Jarda" research/` before every commit touching public HTML.

## Slice 5 — Research pages build

**Appetite.** M–L (expect 4 pages × 15–30 min each).

**Inputs:**
- Slice 2 D11 Wireframe B at [slice-2-blueprint.md:314](docs/plans/prds/2026-04-24-reshape/slice-2-blueprint.md) — representative research-page skeleton.
- Slice 2 D12 dossier aesthetic rule (body class `.research-dossier` + new selectors `.observed`, `.inferred`, `.may-mean`, `.experiment`).
- Peer-cluster research at [codex-R2-C7.md](docs/research/2026-04-21-round-2-research/codex-R2-C7.md) — observations for Ceranna / Avvagraphy / 2 Brides / Honest Guide; structure is already per-peer with public-facts vs inferences.
- Long-range / Paul-Zizka research at [trust-family-business-models.md](docs/research/2026-04-21-round-2-research/trust-family-business-models.md) — 4 archetypes, Zizka template at L71–89, 10-year timeline at L96–130.
- SEO / discovery research at [codex-cluster-*.md, opportunity-scoring.md, codex-R2-C7.md §5-6](docs/research/2026-04-21-round-2-research/).
- Growth-opportunities research — same files; "Ceranna-shaped segment moves" is already a scoped opportunity.

**Output pages (href targets in §6 of index.html):**
1. `research/market-clusters.html` — full peer map. 5 peers × 4 blocks (Observed / Inferred / May-mean / Experiment) per C4 structure. ~800–1000w.
2. `research/ten-year-picture.html` — long-range scenarios, Paul Zizka compounding analysis, 4-archetype framing. ~600w.
3. `research/seo-and-discovery.html` — bilingual-market angles, AEO recipes, one-year moves. ~500w.
4. `research/growth-opportunities.html` — Ceranna-shaped segment moves, 4-stack revenue plan. ~500w.

**Dossier CSS additions** (append to `styles/shared.css`, preserving Slice 3 verbatim-move block + Slice 4 main-brief block grep-identifiable above):
- `body.research-dossier` — bg override (e.g., `--bg-dossier: #f8f5f0` or similar), optional font override for "dossier" feel.
- `.research-header`, `.dossier-humility`, `.back-link` — dossier chrome.
- `.research-block` ALREADY EXISTS in Slice 3 (from pre-reshape site); preserve — D12 is move-not-rewrite.
- `.observed`, `.inferred`, `.may-mean`, `.experiment` — section-level evidence-label styling. Indent + label chip.
- `.research-footer` — WhatsApp footer for research pages.

**Content grounding rule (from Codex market-map-correction P1 finding [codex-cluster-1-market-map.md:205](docs/research/2026-04-21-round-2-research/codex-cluster-1-market-map.md) — lesson still applies):** Every peer observation in the `.observed` block must trace to public-only evidence (website content, published interviews). `.inferred` is clearly-marked speculation. `.may-mean` translates inference into Jarda-specific application. `.experiment` proposes one low-risk Cowork move. Never claim a specific tool/vendor a competitor uses.

**Slice 5 Verification Commands:**
```bash
# All 4 pages exist + non-empty
for p in market-clusters ten-year-picture seo-and-discovery growth-opportunities; do test -s "research/$p.html" || echo "MISSING: $p"; done

# Privacy: no Jarda in any research page
! rg -q "Jarda" research/

# Every page links stylesheet correctly
for p in research/*.html; do rg -q 'href="../styles/shared.css"' "$p" || echo "MISSING stylesheet link: $p"; done

# Every page has body.research-dossier
for p in research/*.html; do rg -q 'class="research-dossier"' "$p" || echo "MISSING dossier body class: $p"; done

# Red-flag grep across research pages (drafted prose scope)
! rg -n '\b(opinionated|convention|as we say|turns out|the truth is|in our view)\b' research/

# WhatsApp anchor in each page footer
for p in research/*.html; do rg -q "WhatsApp" "$p" || echo "MISSING WhatsApp: $p"; done

# Back-link to main page
for p in research/*.html; do rg -q 'href="../index.html"' "$p" || echo "MISSING back-link: $p"; done
```

## Slice 6 — Proofread pass

**Appetite.** S (30–60 min).

**Inputs:**
- Full [voice-audit.md](docs/research/2026-04-24-reshape-research/voice-audit.md) — especially the 3 sample pairs at L270+ and the "doesn't sound like" hit-list at C3.
- [index.html](index.html) and all 4 `research/*.html` pages.

**Checklist:**
1. **Name-leak sweep (blocking):** `rg -q "Jarda" .` across all tracked public files — must return 0 matches.
2. **Red-flag voice grep (blocking):** `rg -n '\b(opinionated|convention|as we say|turns out|the truth is|in our view)\b' index.html research/` — must return 0 matches.
3. **DHH-performed counter-sample sweep:** read every draft passage aloud (or in head). Flag anything that sounds like "Specificity beats breadth" / "Trust compounds slowly" / "clever prompting ages out" — absorb into the "doesn't sound like" column or rewrite.
4. **§1 opening drift check:** the 4-paragraph opening in §1 should still name 5 peer names inline before any video facade. Verify peer_pos < facade_pos.
5. **§4.2 thesis anchoring check:** read 4.2. Verify it names ≥2 peer-cluster names from 4.1 as evidence (currently Ceranna + Paul Zizka).
6. **§4.3 actionability check:** read 4.3. Verify the first move is concrete-enough that Jay Z could start it on Monday (not abstract advice).
7. **§4.4 humility clause B:** verify the WhatsApp anchor appears at the END of §4.4 (last paragraph).
8. **Video-companion copy check:** all 4 summaries start with "Hi Jay Z," and end with "—M" signoff.
9. **Jesse-asked-me decision:** [index.html:31](index.html) (§1 opening) reads "Jesse asked me to map out..." — this is a leftover from the D5 draft in the blueprint. For the Jay Z placeholder version, "Jesse" is coincidentally the name of one of the video creators (Jesse Genet). Decide: keep (mild ambiguity but voice-natural) or rewrite (more defensible but loses a natural opener). Flag for Mark's call.
10. **Copy length audit:** §4.1 ≈250w, §4.2 ≈200w, §4.3 ≈250w, §4.4 ≈150w per D8 budgets. Current state is approximately on-target; verify no drift.

**Known issues to address in Slice 6:**
- The text "style" appears inside a JS comment in the old `index.html` L1099 of the pre-extraction version. After Slice 4 rewrite, the JS block was replaced — this comment may or may not exist. Grep to confirm: `rg -n '<style' index.html` — should only match (if at all) strings inside code blocks. (Pre-Slice-4 we saw one such match; post-rewrite unclear.)
- `href="../styles/shared.css"` in research pages must use `../` prefix since research pages are one level deeper.

## Slice 7 — Ship

**Appetite.** S (30 min).

**Checklist:**
1. **Privacy pre-flight:** `rg -q "Jarda" $(git ls-files '*.html')` must return 0.
2. **Review git log since origin/main:** verify all commits are clean (no accidental backlog files).
3. **Mark-readable check:** open `index.html` + all 4 research pages locally in a browser; click every facade; click peer-cluster anchor; click every §6 pointer.
4. **Push to origin/main:** `git push origin main`.
5. **GitHub Pages rebuild wait:** ~60–90s.
6. **Live verification:** `curl -sSL https://mark-c4r.github.io/Jay-Z/ > /tmp/live.html; ! rg -q "Jarda" /tmp/live.html`.
7. **Jarda handoff:** Mark DMs Jarda the URL + his real-name version (if any) separately.

**IMPORTANT — git init sub-check:** Slice 7 was originally scoped to include `git init` in `jarda-ai-start/` if absent. That's already done (the nested `.git` exists; remote is configured). Skip the `git init` step; just verify with `git remote -v`.

## Known issues / follow-ups (NOT blocking Slices 5-7)

1. **Preflight aggregator relative-path hang — FIXED.** AWF@bf05283 (2026-04-24) normalizes PLAN_FILE to absolute on entry and adds a parent-equals-self guard in the walk-up loop. `git pull origin main` in AWF repo to pick up. Relative-path invocations now complete in <1s. Full rule in LEARNED.md 2026-04-24 ("any `dir=$(dirname "$dir")` walk must use parent-equals-self, not just `!= /`"). If you see orphan preflight processes from earlier sessions: `ps aux | grep preflight-aggregator` → `kill -9 <pid>`.

2. **Slice 4 gate_override reason.** [slice-4-main-page-build.md](docs/plans/prds/2026-04-24-reshape/slice-4-main-page-build.md) frontmatter has `gate_override: auto` for novel-path on `styles/`. Slice 5 will extend styles/shared.css; may need the same override if novel-path fires again, or the directory becomes "not novel" after Slice 4 commits ship to origin (since origin/main then has styles/ commits within 60 days).

3. **JS comment references to old `<style>` block.** Old `renderRail` / state logic was stripped in Slice 4; verify no dangling references.

4. **Thumbnail fallback cascade.** The new index.html uses `maxresdefault.jpg → hqdefault.jpg → 0.jpg`. Pre-reshape used `0.jpg` directly. If max/hq thumbnails 404 for specific videos, the JS cascade handles it, but test in-browser.

## Governance — do not re-litigate

- **Voice anchor:** "Mark writing to one friend over WhatsApp" — strip DHH/37signals cadence. Hi-Jay-Z / you / —M.
- **Red-flag denylist:** `opinionated|convention|as we say|turns out|the truth is|in our view` — zero matches in drafted copy.
- **70/30 video consumption split:** learning videos (Jeff Su, Jack Roberts) = ~150w memory-trigger. Interview videos (Jesse × 2) = ~290–295w stand-alone + 2–3 load-bearing quotes.
- **Per-slice-PRD pivot:** each slice gets its own `/shaping` cycle when its turn comes. Risk score governs depth (Slice 5 is M, likely risk 3–4 — low enough that Codex review is optional; Slice 6 is S; Slice 7 is S).
- **Same-session-ship VA pattern:** rewrite VA rows to post-build state per LEARNED 2026-04-19.
- **Force-track PRDs only, not backlog:** `git add -f docs/plans/prds/…` for each PRD individually. Never `git add docs/` bulk.

## Critical file paths (quick reference)

- **Umbrella plan:** [2026-04-23-jarda-reshape-refresher-primer.md](docs/plans/2026-04-23-jarda-reshape-refresher-primer.md)
- **Slice 2 blueprint (authoritative contract):** [slice-2-blueprint.md](docs/plans/prds/2026-04-24-reshape/slice-2-blueprint.md)
- **Slice 3 PRD:** [slice-3-css-extraction.md](docs/plans/prds/2026-04-24-reshape/slice-3-css-extraction.md)
- **Slice 4 PRD:** [slice-4-main-page-build.md](docs/plans/prds/2026-04-24-reshape/slice-4-main-page-build.md)
- **Research vault (Slice 1 + round 2):** [docs/research/2026-04-24-reshape-research/](docs/research/2026-04-24-reshape-research/) + [docs/research/2026-04-21-round-2-research/](docs/research/2026-04-21-round-2-research/)
- **Memory anchors (user-scope):** `~/.claude/projects/-Users-profile-1-Coding-jarda/memory/` — voice-anchor + video-consumption-split + reshape-memories

## First action in the new session

1. Read this handoff end-to-end.
2. Read Slice 2 blueprint D11 Wireframe B + D12 (dossier aesthetic + token inventory).
3. Invoke `/shaping` on Slice 5 (`--no-research`; Phase C already did research). Expect risk 3, appetite M.
4. Crystallize Slice 5 mini-PRD. Proceed to build.

**HARD PRIVACY GUARD:** before every commit, run `! rg -q "Jarda" index.html research/ 2>/dev/null` — must exit 0.
