---
ticket: jarda#reshape-2026-04-23
status: active
appetite: L
project: jarda
updated: 2026-04-25
supersedes: jarda-ai-start/docs/plans/2026-04-21-v2-restructure.md
risk_score: 6
phase_e_completed: 2026-04-25  # Slices 6 + 7 shipped + live verified; see follow-on handoff
follow_on: docs/plans/2026-04-25-session-handoff-post-phase-e.md
files:
  - jarda-ai-start/index.html
  - jarda-ai-start/research/*.html (new)
  - jarda-ai-start/practical/index.html (new — DESCOPED during execution; resume decision pending in follow_on doc)
  - jarda-ai-start/assets/shared.css (new — extracted)
  - jarda-ai-start/docs/research/2026-04-24-reshape-research/*.md (new)
  - jarda-ai-start/docs/design/2026-04-24-reshape/*.md (new)
---

# Jarda site reshape — refresher primer, not first-touch e-learning

## Context

The Jay-Z site shipped on 2026-04-23 (Phase-E) with a 6-stop / 3-block architecture, hand-picked transcript highlights, 3 curated "Teaching voices" videos cut into narrow time-windows, and a single-scroll research appendix (Blocks D–G). Today's re-review surfaced extensive feedback: the site reads as "20 students delivering isolated pieces of homework, glued together" — no cohesion, videos treated as raw material to be mined for 2% excerpts, IA vocabulary (`Stop N of 6 · Block N of 3`) obscures meaning, 24 unshipped research docs + 370KB of transcripts sit unsurfaced, pacing assumes first-touch teaching. Voice over-steered toward DHH / 37signals / Basecamp cadence — too performed, not matching the casual register of the source videos.

**New anchoring data** (surfaced during clarification round): Jarda's prior video consumption is **split by video type**:
- **Learning videos** (Jeff Su `z9rdrNrkvDY`, Jack Roberts `cNf7uVff11Y`): ~70% watched. Refresher-posture correct — summaries trigger memory, chapters ground navigation.
- **Interview/talk videos** (Jesse Genet a16z `yiJOTCRVWjc`, Jesse Genet Cognitive Revolution `aFQskhdR3RQ`): ~30% watched. Closer to first-touch — prose summaries must stand on their own, not just trigger memory. Master sections do more teaching lift for this group.

The site serves **two intertwined jobs** delivered as a single progressive flow:

1. **Refresher + launchpad for AI** — video companion for concepts already watched (learning videos, ~70% exposure) plus lighter-touch teaching for the interview content (~30% exposure), Cowork setup pointers, enough basic intro to get excited and equipped.
2. **Client-style competitive-intelligence brief** — Jarda is framed like a client who hired us to review his business and asked how he could apply AI. Deliver: strengths/weaknesses sketch, surface-level opportunity intel, Cowork-vs-Code applied-to-his-business framing, guided prompts to practice. Humility clause: the intel is surface-level; if any vector resonates, we recommend a single-vector deep dive.

**Primary gap hypothesis (compass for Slice 1 spikes):** the dominant gap is **identity → action**, in that order. Comprehension is mostly solved for the learning-video group and partially solved for the interview group; the reshape needs to close the comprehension gap on interviews (via stand-alone prose summaries), but the load-bearing gap is that the current site reads as a beautiful explainer for Generic Small Business Owner — fails the made-for-me test, which gates Jarda's first Cowork session. Trust is mostly carried by friend-channel. Slice 1 research spikes and Slice 2 blueprint must serve identity → action first; comprehension second (interviews > learning videos); trust as a background constraint, not a focus. Hypothesis is subject to revision from Slice 1 findings but must be the starting frame, not left open.

**Intended outcome:** Pivot purpose from "teach Jarda from scratch" to "refresh + scaffold + brief." Rebuild IA around progressive information load: AI intro → Cowork setup → brief exec-summary + opportunity intel → guided practice → deep appendix. Chapter-anchor video accompaniment (no more transcript mining). Demote the research appendix to "appendix of an appendix" — source material for the brief, not primary reading. Strip DHH/Basecamp voice over-steering; anchor voice to **"Mark writing to one friend over WhatsApp"** (the WhatsApp-feedback footer already sets this register); proofread each artifact for voice drift before shipping.

**Format decision is research-first.** Before committing to single-page progressive flow vs main + sibling pages, Slice 1 runs three format-best-practices spikes in parallel: (a) self-paced e-learning structure/navigation/attention patterns, (b) exec-summary / client-brief / competitive-intelligence delivery format, (c) single-reader personal-brief / private-memo / "I-wrote-this-for-you" genre patterns. Slice 2 blueprint crystallizes structure from findings — don't pre-commit. **Where the N=1 personal-brief spike conflicts with N≥10 e-learning or exec-summary norms, N=1 wins** (this plan is one letter to one named friend, not a course or a deliverable).

## Appetite

**L (co-shape + approve + midpoint + ship).** Multi-session. Shape → research → build across 2–3 build sessions → ship.

## Risk score: 6 / 8 (High)

- Novelty 2: reshape pattern familiar; refresher-as-primary purpose is new framing
- Reversibility 1: single repo, git-reversible
- Dependencies 1: GitHub Pages, no external breakage surface
- Interface uncertainty 2: taste-layer calls, audience = 1 named friend, preferences inferred from owner

Risk ≥ 4 → MANDATORY cross-model review gates (on plan AND on reshape draft).

## Solution sketch

### Purpose statement (draft — refine in Slice 2)

> These are notes I put together while going through the intro AI-agents material with you in mind. You've already seen the videos — this is a refresher, a note-pad, and a quick look at where AI could fit in your business. The video chapters ground the concepts. The brief reads your business from a distance and points at a handful of opportunities — surface-level, not exhaustive. If one rings the bell, we can go deeper. Guided prompts at the end hand you something to try.

Final wording drafted in Slice 2 from Slice-1 voice-audit findings. Watch for DHH/Basecamp over-steering; match the casual register of the source videos.

### Candidate site structure (provisional — locked in Slice 2)

Progressive information load. Exact surface split (single page vs main + siblings) decided from Slice-1 e-learning + exec-summary format research. Candidate layout:

```
/  (main — progressive flow, Jarda reads top-to-bottom)
    §1 Intro             — what this is / how made / how to use / humility note
    §2 AI orientation    — video companion: self-learning group (Jeff Su, Jack Roberts)
                           + interviews group (Jesse Genet ×2)
                           master-section chapters + prose summaries, NO transcript mining
    §3 Cowork setup      — Cowork-vs-Code framing, why Cowork first for Jarda
    §4 Business brief    — exec-summary: strengths, weaknesses, opportunities (surface-level)
                           + Cowork applied to his business + humility clause
                           + "if any vector resonates, deep dive recommended"
    §5 Guided practice   — 4–6 paste-ready prompts anchored to brief findings + videos
    §6 Deep appendix     — pointers to /research/*.html; framed as "appendix of an appendix"

/research/market-clusters.html       → deep source: market research (Block D + codex cluster 1)
/research/growth-opportunities.html  → deep source: funnel/SEO systematization (Block E + cluster 6)
/research/seo-recipes.html           → deep source: Cowork prompts + SEO patterns (Block F/F+)
/research/ten-year-picture.html      → deep source: privacy/legal (Block G, GDPR pruned)
```

Why provisional: Slice 1 Spike A (e-learning patterns) + Spike B (exec-summary / client-brief format) may surface a layout (e.g. split `/learn/` + `/brief/`) that reads better than single-page progressive. Decide in Slice 2 from findings. If single-page progressive wins, `/practical/index.html` folds into `§5 Guided practice` (no separate surface). If multi-page wins, keep `/practical/` and sequence it main → practical → research.

### Video accompaniment paradigm (chapter-anchored, refresher-oriented)

Each video section provides:

1. **Prose summary** (~150 words) — what this video covers, why it's in the curriculum, what Jarda should take away. Serves as memory-trigger for the already-watched video.
2. **Master-section chapter tree** — universal ~6 master sections per video regardless of source chapter count:
   - `z9rdrNrkvDY` (Jeff Su, 9 source chapters): ~6 master sections, light consolidation
   - `cNf7uVff11Y` (Jack Roberts, 43 source chapters): ~6–8 master sections, heavy consolidation (group related chapters)
   - `yiJOTCRVWjc` (Jesse Genet a16z, 8 source chapters): ~6 master sections, light consolidation
   - `aFQskhdR3RQ` (Jesse Genet Cognitive Revolution): chapters TBD during Slice 1; target ~6 master sections
3. **Per master-section row:** click-to-jump timestamp + 1-2 sentence descriptor. Source chapters may nest under master sections for drill-down navigation if volume warrants.
4. **NO transcript-mined highlights.** Chapter-anchored only. If a video has sparse chapters, self-produce master sections during Slice 1 review; don't invent fine-grained highlights.

### Vocabulary + voice

**Vocabulary:**
- `Stop N of 6` → TBD in Slice 2 from Spike A e-learning norms. Removes the non-standard "stop" metaphor.
- `Block N of 3` → removed entirely. Was internal IA, not user-facing.
- `Try one` prompt blocks → consolidate into `§5 Guided practice`. Don't sprinkle after every video section.
- `Go Deeper` branches → audit each of the 24 current branches; prune aggressively. Target ≤1 per section, only where the branch genuinely adds useful depth. Dead-end rabbit holes removed.

**Voice — strip over-steering:**

Current site over-indexed on DHH / 37signals / Basecamp voice guidance. User feedback: "overdone it too much." Target register is **"Mark writing to one friend over WhatsApp"** — the WhatsApp-feedback footer already sets this tone; extend it through the whole document. Casualness matching the video source material is secondary texture, not the anchor. No brand voice mimicry, no performed opinionated-ness, no aphorism cadence, no N-reader educational voice. Claude's default voice when unguided is usually fine.

Operationalized as:
- **Slice 1**: voice audit of current site. Flag DHH-style mimicry AND N-reader-educational tone (where it should be N=1 letter-to-one-friend).
- **Slice 2**: blueprint decides voice posture. Anchor: "Mark writing to one friend over WhatsApp." Includes 2–3 "sounds like / doesn't sound like" sample pairs so drafters have a concrete target.
- **Slices 3–5**: each artifact proofread after drafting against the WhatsApp-anchor + sample pairs. Flag: performed cadence, unearned opinionated-ness, brand-voice borrowing, N-reader educational tone.
- **Slice 7**: final voice proofread pass across all shipped surfaces against the WhatsApp-anchor.

### Tactical cleanup (bundled into macro)

- **Footer nav removal:** drop `.bn-prev`, `.bn-next`, `.bn-jump`, `.page-footer` mailto ("Stuck? Reply to the email..."). Replace with minimal footer: "Last updated · feedback via WhatsApp (you know where to find me)."
- **"Why these six stops?" section:** absorbed into new intro block as a compressed "how this was made" note. Remove from appendix.
- **GDPR / France-law / California SB detail:** compress to 2–3 sentence mention on `/research/ten-year-picture.html`. Current full paragraph pruned.
- **Stop 6 Block 2 reading** (`stop-6-block-2`): relocate privacy content to ten-year-picture page; Stop 6 itself collapses into the interviews group.
- **Customization-ack / Jay-Z persona:** retain but move out of C7.2 slot → surface naturally in intro purpose statement. Kill placeholder feel.

## Critical files

### Read / reuse / supersede

- `jarda-ai-start/index.html` — full body rewrite. Current patterns to reuse: `.yt-facade` video thumbnail pattern + iframe-on-click (line ~1900 area), `videoChapters` JS object structure (lines 2280–2348), `.research-block` styling (reuse where appropriate on new appendix pages).
- `jarda-ai-start/docs/plans/2026-04-21-v2-restructure.md` — add `status: superseded`, `superseded-by:` pointer to this plan's eventual `docs/plans/` copy.
- `jarda-ai-start/docs/plans/prds/2026-04-22-round-2/INDEX.md` — archive as historical; reference in new research notes.
- `docs/transcripts/*.txt` (7 files, ~370KB) — source for master-section consolidation prose summaries (Jeff Su: `jeff-su-cowork-80pct.txt`; Jack Roberts: `jack-roberts-cowork-course.txt`; Jesse Genet: 3 `jesse-*.txt` files + `.vtt` captions).
- `jarda-ai-start/docs/research/2026-04-21-round-2-research/*.md` (24 files) — source material for expanded research pages:
  - `codex-cluster-1-market-map.md` → feeds `market-clusters.html`
  - `codex-cluster-6-appendix-depth.md` → feeds `growth-opportunities.html` + cross-page depth
  - `gear-lists-business-research.md` → feeds `seo-recipes.html`
  - `trust-family-business-models.md`, `opportunity-scoring.md`, `scoring-codex.md`, `scoring-gemini.md` → distributed across research pages per topical fit
  - `kid-privacy-best-practices.md` → feeds `ten-year-picture.html`
- `/Users/profile_1/.claude/projects/-Users-profile-1-Coding-jarda/memory/` — past-conversation memory for Slice 1 archaeology.
- `CONTEXT.md`, `UNFINISHED-WORK.md`, `NEXT-SESSION-FEEDBACK.md` — existing site navigation docs; update in Slice 7.

### New files

- `jarda-ai-start/research/market-clusters.html`
- `jarda-ai-start/research/growth-opportunities.html`
- `jarda-ai-start/research/seo-recipes.html`
- `jarda-ai-start/research/ten-year-picture.html`
- `jarda-ai-start/practical/index.html`
- `jarda-ai-start/assets/shared.css` — extract shared styles from inline `<style>` in current `index.html` for reuse across main + research + practical pages
- `jarda-ai-start/docs/research/2026-04-24-reshape-research/memory-archaeology.md`
- `jarda-ai-start/docs/research/2026-04-24-reshape-research/source-material-rescan.md`
- `jarda-ai-start/docs/research/2026-04-24-reshape-research/e-learning-patterns.md` (Spike A)
- `jarda-ai-start/docs/research/2026-04-24-reshape-research/exec-summary-patterns.md` (Spike B)
- `jarda-ai-start/docs/research/2026-04-24-reshape-research/personal-brief-patterns.md` (Spike C)
- `jarda-ai-start/docs/research/2026-04-24-reshape-research/voice-audit.md`
- `jarda-ai-start/docs/research/2026-04-24-reshape-research/line-by-line-ux-review.md`
- `jarda-ai-start/docs/research/2026-04-24-reshape-research/post-draft-review.md`
- `jarda-ai-start/docs/design/2026-04-24-reshape/blueprint.md`
- `jarda-ai-start/docs/design/2026-04-24-reshape/wireframes/*.html`

## Verified assumptions

| Claim | Source | Status |
|-------|--------|--------|
| 4 videos in use, IDs `z9rdrNrkvDY` / `cNf7uVff11Y` / `yiJOTCRVWjc` / `aFQskhdR3RQ` | `jarda-ai-start/index.html` videoChapters object (lines 2280–2348) | ✓ verified 2026-04-23 |
| Stops 1–4 use one Jeff Su video cut into 4 windows; Stop 5 bundles Jack + Jesse a16z; Stop 6 is Jesse Cognitive Revolution | IA audit (Explore agent) | ✓ verified 2026-04-23 |
| Research appendix (Blocks D–G) in single `<section id="research">` with no tabs/pagination | IA audit | ✓ verified 2026-04-23 |
| Transcript corpus at `docs/transcripts/` (7 files ~370KB) | Source-material inventory | ✓ verified 2026-04-23 |
| 24 unshipped research docs at `jarda-ai-start/docs/research/2026-04-21-round-2-research/` | Source-material inventory | ✓ verified 2026-04-23 |
| GitHub Pages supports multi-HTML-file structure | Known behavior; repo deploys static HTML already | ✓ known; re-verify at Slice 4 preview |
| YouTube chapter metadata publicly accessible for all 4 video IDs | YouTube standard API; requires confirmation | **PENDING — verify during Slice 1** |
| Jarda watched ~70% of learning videos (Jeff Su, Jack Roberts) and ~30% of interview/talk videos (Jesse Genet ×2) | User statement 2026-04-23 (refined from initial "at least the shorter videos") | ✓ confirmed 2026-04-23 |
| Cross-model challengers (Codex CLI, Gemini CLI) available in environment | SessionStart hook report | ✓ confirmed this session |

## Process revision (2026-04-23, mid-Slice-1)

**Status at revision:** Slice 1 is ~90% shipped (memory archaeology, rescan, Spikes A/B/C, voice audit, 3-reviewer UXR + synthesis all on disk). Video-companion drafts landed only for Jack Roberts (`video-companion-drafts.md`, 2.8KB); Jeff Su + both Jesse Genet drafts missing — background agents returned "done" without writing. Two compacts have folded context on this single ticket.

**Status at 2026-04-23 (end of day):** Slice 1 fully shipped (10/10). Jeff Su + Jesse a16z + Jesse CR video-companion drafts direct-written into `video-companion-drafts.md` (now ~15KB, 4 sections). YouTube chapter JSON artifacts cached on disk at `chapters/{z9rdrNrkvDY,yiJOTCRVWjc,aFQskhdR3RQ}.json`. Red-flag voice grep returns zero matches across the 3 new sections. Research dir remains gitignored per `jarda-ai-start/.gitignore:18` (`research/`) — artifacts live on disk, not committed. Phase B checkpoint pending user sign-off before Slice 2 shaping.

**Decision:** upgrade process discipline. Risk-6 mandates cross-model review anyway; each remaining slice carries enough weight to deserve its own PRD + Codex/Gemini pass rather than executing off the umbrella plan. Ship-as-we-go is fraying — drafts get lost across compacts.

**Revised forward path:**
1. **Finish Slice 1** by direct-drafting (no agent delegation) the 3 missing video-companion entries (Jeff Su memory-trigger ~150w; Jesse Genet a16z + CR stand-alone ~250–300w with load-bearing quotes).
2. **Slice 1 checkpoint** with user (plan's original demo prompt).
3. **Switch to per-slice PRD mode** for Slices 2–7. Each slice gets:
   - A standalone PRD at `jarda-ai-start/docs/plans/prds/2026-04-24-reshape/slice-N-<slug>.md`
   - Explicit verified-assumptions table (grep-checked)
   - Codex CLI plan-review (mandatory per risk ≥ 4)
   - User approval before that slice's build starts
4. Umbrella plan (this file) becomes the index; per-slice PRDs become source of truth for execution.

Trades throughput for drift resistance — correct trade for a risk-6 L-ticket with taste-layer calls and a single reader.

## Execution slices

### Slice 1 — Research + audit 🔼 (uphill)

Groundwork. Everything else depends on this. Before any structure/format commitment, run **three format-best-practices spikes in parallel** (A: e-learning, B: exec-summary, C: single-reader personal-brief) so Slice 2 blueprint is grounded, not guessed. N=1 personal-brief spike wins where it conflicts with N≥10 norms.

**Tasks:**
1. **Memory archaeology** — read `/Users/profile_1/.claude/projects/-Users-profile-1-Coding-jarda/memory/` + `docs/session-logs/*.md` for original design intent, decisions made/rejected, prior prompts and corrections.
2. **YouTube chapter + description fetch** for all 4 video IDs (yt-dlp or YouTube API). Verify accessibility. If any video has zero chapters, flag for self-produced master-sectioning.
3. **Master-section consolidation** per video (target ~6 sections; heavy consolidation for 43-chapter video, light for 8/9-chapter videos). Interview-group master sections (Jesse Genet ×2) do more teaching lift than learning-group master sections — they must hold concepts standalone because Jarda only watched ~30% of this material.
4. **Prose summaries — posture split by video type:**
   - Learning videos (Jeff Su, Jack Roberts): ~150 words each, memory-trigger posture (Jarda saw ~70%).
   - Interview/talk videos (Jesse Genet ×2): ~250–300 words each, stand-alone posture — reader must get the concept even if he never watches (~30% watched). Include the 2–3 load-bearing quotes that make the concept land without the video.
5. **Spike A — self-paced e-learning best practices** (web research, cap ~2 hours, 3 canonical sources — Julie Dirksen / Mike Caulfield / Coursera-edX-Obsidian pattern analyses). Questions: vocabulary norms (section / lesson / module / chapter), pacing + chunking patterns, navigation / TOC patterns, attention + engagement do's and don'ts, companion-content patterns (video + text), progressive-disclosure patterns, appendix / handoff transitions, practical-application handoffs. Output: `e-learning-patterns.md` with "candidate structures + recommendation."
6. **Spike B — executive-summary / client-brief / competitive-intelligence delivery format** (web research, cap ~2 hours, 3 canonical sources — McKinsey/BCG-style exec-summary patterns, consultant-deliverable norms, competitor-teardown review formats, "advisor-to-owner" brief patterns). Questions: how long? what sub-sections? how much detail? tone? opening hook? handoff to appendix? how to land epistemic humility without undercutting authority? how to invite deeper single-vector inquiry without over-promising? how to weave in Cowork-vs-Code framing and guided prompts? Output: `exec-summary-patterns.md` with "candidate structures + recommendation."
7. **Spike C — single-reader personal-brief / private-memo genre** (web research, cap ~1 hour, 3 canonical sources — Tufte-style one-off handoffs, "I-wrote-this-for-you" private memos, personal-letter-as-deliverable patterns, published examples of one-named-friend documents). Questions: how does N=1 voice differ from N≥10? how does reader-texture show up (named details, shared history, in-jokes)? where does the writer's first person belong (opening / closing / scattered)? how long before N=1 starts feeling performed? when do N=1 patterns override e-learning and exec-summary norms? Output: `personal-brief-patterns.md` with "override map" — where N=1 patterns trump Spike A / B findings.
8. **Voice audit of current live site** — read https://mark-c4r.github.io/Jay-Z/ top-to-bottom. Flag every line where DHH / 37signals / Basecamp voice borrowing surfaces: performed opinionated-ness, aphorism-style cadence, contrarian positioning, Rework-style brevity-as-performance. Also flag lines that read as N-reader educational rather than N=1 letter-to-one-friend. Output: `voice-audit.md` with flagged lines + casual-default rewrites in the target register ("Mark writing to one friend over WhatsApp").
9. **Line-by-line UX review of current live site** — dispatch 3 parallel reviewers per user's explicit ask:
   - Codex CLI: architecture/methodology lens (per `~/.claude/agents/codex-challenger/AGENT.md`)
   - Gemini CLI: UI/design lens (per `~/.claude/agents/gemini-challenger/AGENT.md`)
   - Explore agent with UX-researcher framing: user-experience lens
   - Common prompt: "Read https://mark-c4r.github.io/Jay-Z/ top-to-bottom, section-by-section, line-by-line. Does what's on the page make sense? Where does it confuse, mislead, or waste attention? Call out specific lines/blocks. Separately flag: any voice that reads as performed / borrowed / over-polished rather than casual-matching-video-register, or N-reader educational rather than N=1 personal letter."
10. **Synthesize** into research docs under `jarda-ai-start/docs/research/2026-04-24-reshape-research/`: `memory-archaeology.md`, `source-material-rescan.md`, `e-learning-patterns.md` (A), `exec-summary-patterns.md` (B), `personal-brief-patterns.md` (C), `voice-audit.md`, `line-by-line-ux-review.md`.

**Demo:** 7 research docs committed. User-facing checkpoint: "Here's what the archaeology + three format spikes + voice audit + cross-model review surfaced. Go/no-go on direction before I draw the blueprint."

**Files:** `jarda-ai-start/docs/research/2026-04-24-reshape-research/{memory-archaeology,source-material-rescan,e-learning-patterns,exec-summary-patterns,personal-brief-patterns,voice-audit,line-by-line-ux-review}.md`

**Depends on:** Plan approval.

### Slice 2 — Blueprint + wireframes + vocabulary + voice 🔼 (uphill)

Crystallize the format from Slice 1 spike findings. No pre-commitment on single-page-vs-multi-page before research lands.

**Tasks:**
1. **Structure decision** — review Spike A (e-learning patterns) + Spike B (exec-summary patterns) + Spike C (personal-brief/private-memo patterns); pick single-page progressive flow vs main + sibling pages. Where N=1 personal-brief (C) conflicts with A/B, C wins. Document rationale from research findings.
2. **Section ordering decision** — test AT LEAST these two ordering variants against Slice 1 findings + the identity→action compass:
   - (a) Canonical: §1 intro → §2 AI orientation (learning + interviews) → §3 Cowork setup → §4 business brief → §5 guided practice → §6 appendix
   - (b) Teaser-forward: §1 intro → §2 brief teaser (2–3 sentences naming 3 opportunities) → §3 AI orientation → §4 Cowork setup → §5 full brief → §6 guided practice → §7 appendix
   The teaser-forward variant addresses UXR concern that canonical order risks losing Jarda at §3 Cowork setup (tool-meta paragraph) before he reaches the made-for-him payoff. Pick one; document why. This is a named alternative decision, not a discovered one.
3. **Vocabulary** (section / lesson / etc.) decided from Spike A, filtered through Spike C.
4. **Voice posture** decided from voice-audit + Spike C + "Mark writing to one friend over WhatsApp" anchor (the WhatsApp-feedback footer already sets this register). Draft 1-paragraph voice guidance + **2–3 "sounds like / doesn't sound like" sample pairs (~50 words each)** so drafters have a concrete target, not an adjective list. Required: at least one "sounds like" sample and one "doesn't sound like DHH-performed" counter-sample.
5. **Opening-90-seconds contract** (Slice 2 acceptance criterion — NOT negotiable): §1 intro must answer in this order, in roughly this much space:
   - (a) Who made this + why — first-person, 2 sentences, names Mark explicitly.
   - (b) What it is for Jarda specifically — refresher + brief on his business, 1–2 sentences.
   - (c) One immediate payoff that justifies the scroll — a concrete teaser ("§4 has three opportunities I'd test first if this were my business" or equivalent from the brief findings).
   Draft opening-90s copy (~150 words) must be committed as part of blueprint, not deferred to Slice 3 build.
6. **Master-section titles + timestamps** locked per video. Interview-group (Jesse Genet ×2) titles weight-toward stand-alone concept naming; learning-group titles can lean memory-trigger.
7. **IA blueprint** — full section-by-section outline per chosen ordering (task 2). Include draft section copy (~100 words per section) for intro and the business-brief handoff.
8. **Exec-summary brief outline** (from Spike B + Spike C override) — 3–5 sub-sections (e.g. business at-a-glance, strengths, weaknesses, opportunities, Cowork applied). Word budget per sub-section.
9. **Humility clause — two placements, not one:**
   - Top of §4 (one sentence): frame the brief as surface-level, honest about that.
   - End of §4 (two sentences): concrete next step language — "if X rings the bell, here's how I'd approach a focused week on it."
   Single-instance framing reads as either throat-clearing or apology; split reads as honest framing + invitation. Draft both in Slice 2.
10. **Go Deeper audit criterion** — upgrade from "target ≤1 per section if useful" (N-reader taste) to **"would Jarda click this?"** (N=1 test). Expect to kill >80%, not prune to 1-per-section. Document survivors with per-branch reason.
11. **Wireframes** — main page HTML skeleton; one representative research page (`market-clusters.html`); if structure decision is multi-page, also `practical/index.html`.
12. `shared.css` style extraction plan.

**Demo:** Blueprint + wireframes committed. Checkpoint prompt: "Structure decision locked from research. Sign off on blueprint + voice posture before build?"

**Files:** `jarda-ai-start/docs/design/2026-04-24-reshape/blueprint.md` + wireframes under same dir.

### Slice 3 — Main page rewrite 🔽 (downhill once blueprint is locked)

**Tasks:**
1. Extract shared styles from current inline `<style>` → `assets/shared.css`.
2. Rewrite `index.html` body per blueprint: §1 intro → §2 AI orientation (self-learning group + interviews group) → §3 Cowork setup → §6 appendix handoff (at minimum). §4 brief + §5 guided practice land in Slice 5 (or fold into this Slice if Slice 2 chose single-page-progressive).
3. Rebuild `videoChapters` JS object around master-section structure.
4. Reuse `.yt-facade` click-to-iframe pattern unchanged.
5. Implement new vocabulary in `.stop-meta` equivalent.
6. Remove footer nav (`.bn-prev`, `.bn-next`, `.bn-jump`, `.page-footer` mailto).
7. Consolidate Try-blocks into `§5 Guided practice`; no mid-video Try sprinkles.
8. Audit and prune Go Deeper branches per new quality bar (target ≤1 per section, only if genuinely useful).
9. **Voice proofread** — re-read drafted sections end-to-end. Flag performed cadence, DHH mimicry, borrowed aphorisms. Rewrite flagged lines to casual default.

**Demo:** Local preview via `python3 -m http.server`. Side-by-side with current live site.

**Files:** `jarda-ai-start/index.html`, `jarda-ai-start/assets/shared.css`.

### Slice 4 — Deep appendix pages (appendix of an appendix) 🔽

These are the source material the brief in §4 + guided prompts in §5 point TO — not primary reading. Framing: "if a vector from the brief resonates, this is the deeper material; if you want a real deep dive, we recommend redoing the research with single-vector focus (SEO, YouTube, travel editorial, etc.)."

**Tasks:**
1. Build 4 research pages sharing `shared.css`:
   - `market-clusters.html` ← Block D + `codex-cluster-1-market-map.md` + relevant unshipped market research
   - `growth-opportunities.html` ← Block E + `codex-cluster-6-appendix-depth.md`
   - `seo-recipes.html` ← Block F/F+ + `gear-lists-business-research.md`
   - `ten-year-picture.html` ← Block G (GDPR/France/SB1247 compressed) + `kid-privacy-best-practices.md`
2. Each page: **humility header** (~50 words: "surface-level scan; deep-dive recommended if this vector resonates; here's how we'd approach a single-vector version") + summary + drill-down + "back to main" link + cross-link to sibling research pages.
3. Verify GitHub Pages multi-page routing works (test locally, then stage commit + preview).
4. **Voice proofread** — each page reviewed for drift.

**Demo:** Local preview — click through main → each research page → back.

**Files:** `jarda-ai-start/research/{market-clusters,growth-opportunities,seo-recipes,ten-year-picture}.html`.

### Slice 5 — Business brief + Cowork setup + guided practice 🔼 → 🔽

The competitive-intelligence half of the deliverable. Exact surface location — inline in main `index.html` §3–§5 OR separate `practical/index.html` — set by Slice 2 structure decision.

**Tasks:**
1. **§3 Cowork setup** — ~200 words on Cowork-vs-Code: why Cowork first for Jarda (lower setup bar, matches his current working style, covers 80% of what he needs from videos he's already watched); Code framed as "needs more setup, come back when a real project wants it."
2. **§4 Business brief** — exec-summary synthesized from the 24 unshipped research docs + Block D/E/F/G content, structured per Slice 2 Spike B outline filtered through Spike C personal-brief overrides (likely: business at-a-glance, strengths, weaknesses, opportunities, Cowork applied to his business). Surface-level intentionally. Word budget set in Slice 2 blueprint (target ~800–1200 words total).
3. **Jarda-specific detail in the brief (made-for-him shown, not claimed)** — pull at least 1–2 concrete Jarda-specific references into the opportunities section: WhatsApp phrases he's actually used, his actual site URL, a business-specific line only this document could carry. Audit sources: WhatsApp chat history (if accessible), his website, the memory archaeology from Slice 1. If zero detail is pullable, flag during Slice 5 and escalate — identity→action is the primary gap and generic opportunities fail it.
4. **Humility clause** positioned per Slice 2 decision (two placements — top framing + bottom invitation). Top language: "this is a surface-level scan from a distance, not a charged deep-dive; standing behind it but honest about what it is." Bottom language: "if any of these rings the bell, that's when a focused week on that one vector would pay off — can suggest how to approach it."
5. **§5 Guided practice** — 4–6 paste-ready prompts Jarda can drop into Claude Cowork. Each anchored to a brief finding or video concept. Prompts are the actionable handoff — if he only does one thing after reading, the prompts are it. At least one prompt should reference Jarda-specific business detail (not generic "[your business]" placeholder).
6. **Handoff** — "Ping me on WhatsApp if you hit a wall." No email, no "reply to the email I sent you," no inappropriate formality.
7. **Voice proofread** — brief + Cowork section + prompts. Performance / brand-mimicry / N-reader educational tone flagged + rewritten to "Mark writing to one friend over WhatsApp" register.

**Demo:** Local preview. User reviews before cross-model review in Slice 6.

**Files:** `jarda-ai-start/index.html` §§3–5 (if single-page) OR `jarda-ai-start/practical/index.html` (if multi-page, per Slice 2 decision).

### Slice 6 — Cross-model review of reshape draft 🔽

Pre-ship gate (MANDATORY per risk ≥ 4).

**Tasks:**
1. Dispatch Codex CLI on reshape draft (all new/rewritten files). Prompt: plan-review protocol, look for P1 blockers, methodology issues, architecture concerns.
2. Dispatch Gemini CLI on reshape draft. Prompt: UI/design review, does the new IA make sense, does the refresher framing land.
3. Fold findings. If P1 blockers surface, loop back to relevant slice. Round cap: 2.

**Demo:** Fold summary committed. Go/no-go on ship.

**Files:** `jarda-ai-start/docs/research/2026-04-24-reshape-research/post-draft-review.md`.

### Slice 7 — Polish + final voice pass + ship 🔽

**Tasks:**
1. Full link audit across main + 4 research pages (+ practical page if separate). No 404s.
2. **Final voice proofread across all surfaces** — one end-to-end sweep against the "Mark writing to one friend over WhatsApp" anchor + Slice 2 sample pairs. Flag: DHH / 37signals / Basecamp drift, performed cadence, N-reader educational tone. Any flagged line rewritten to the WhatsApp register.
3. Screenshot pipeline: before/after captures for documentation.
4. Update `CONTEXT.md`, `UNFINISHED-WORK.md`, `INDEX.md` to reflect new state.
5. Supersede `jarda-ai-start/docs/plans/2026-04-21-v2-restructure.md`: set `status: superseded`, `superseded-by:` → this plan's `docs/plans/` copy.
6. Commit + push.
7. Verify GitHub Pages deployment at https://mark-c4r.github.io/Jay-Z/ + each sub-page URL.
8. WhatsApp ping to Jarda (informal feedback round).
9. Write retro note.

**Demo:** Live site matches design. Retro committed.

## Rabbit holes

- **Self-produced finer chapters for low-chapter videos** — could balloon into full re-chaptering. Cap: master-section count per video is 6 ± 2. If source has fewer chapters than 4 and no natural subdivisions, accept fewer master sections.
- **Writing new research content for appendix pages** — 24 unshipped research docs exist but are raw. Cap: light rewrite + consolidation, not full new research. Fresh research beyond collected material → defer to v1.5.
- **Spike A (e-learning best practices)** — could spiral. Cap: 3 canonical sources, ~2 hours. Stop when vocabulary + structure + pacing decisions are grounded.
- **Spike B (exec-summary / client-brief format)** — same cap: 3 canonical sources, ~2 hours. Stop when structure + humility-clause pattern + handoff approach are decided.
- **Spike C (single-reader personal-brief / private-memo genre)** — tightest cap: 3 canonical sources, ~1 hour. Output is an "override map" showing where N=1 trumps Spike A/B — not a standalone genre treatise. Stop when the override rules are clear.
- **Business brief depth** — the temptation is to make the brief comprehensive. Cap: ~800–1200 words total, surface-level by design, with humility clause + deep-dive invitation. Comprehensive analysis belongs to a future single-vector deep-dive engagement, not v1.
- **Cowork-vs-Code framing** — Cowork-vs-Code is deep. Cap: ~200 words. Anchor to "basic intro + Jarda's current context"; don't attempt comprehensiveness.
- **Shared CSS extraction** — easy to over-engineer into a full design system. Cap: extract only what's reused across ≥2 pages. Inline one-offs stay inline.
- **Voice engineering** — the fix is to REMOVE over-steering, not to add new voice guidance. Cap: strip DHH/Basecamp mimicry; default to casual; don't invent a new voice system. Claude's default voice when unguided is usually fine.
- **Cross-model review round 3** — requires a named directional contradiction per shape-up rule. Do NOT run round 3 unless reviewers disagree on shape-changing direction. Default: round cap 2.

## No-gos

- No new video sourcing (reuse the 4 existing IDs only)
- No transcript re-generation (existing transcripts are source of truth)
- No custom domain / analytics / CMS migration
- No build system beyond what GitHub Pages serves natively
- No new major features from v1.5 deferred list (Video Cards, Practitioners sidebar, Market Intel deepening beyond existing research docs) — stay deferred
- No changes to video embed mechanism (keep `.yt-facade` + iframe-on-click pattern)
- No changes to deployment workflow
- No responsive redesign beyond what multi-page layout minimally requires

## Verification

### Before ship (Slice 6 → Slice 7 boundary)

- Cross-model review complete (Codex + Gemini), all P1 blockers resolved or documented
- Local preview verified on desktop viewport (mobile check deferred unless Jarda accesses mobile — confirm during Slice 7)
- Link audit: every internal link resolves
- All 4 research pages render correctly in local preview + each carries a humility header
- Business brief (§4) renders with humility clause prominent
- Guided-practice prompts (§5) render with paste-ready formatting
- Main page intro renders correctly; purpose statement prominent
- Video chapter click-to-jump verified: spot-check 3 master sections per video (12 total)
- Footer cleaned: no mailto, no A/B/Prev/Next nav, no "Stuck? Reply to the email"
- GDPR paragraph pruned to 2-3 sentences on ten-year-picture page
- "Why six stops" section removed from bottom, relevant framing absorbed into intro
- No "Stop N of 6 · Block N of 3" vocabulary surviving anywhere in new HTML
- **Final voice pass** — end-to-end read across all surfaces for DHH / 37signals / Basecamp drift. Every flagged line rewritten to casual register before ship.

### After ship (Slice 7 post-deploy)

- Live site at https://mark-c4r.github.io/Jay-Z/ matches local preview
- All sub-page URLs resolve (200 status):
  - https://mark-c4r.github.io/Jay-Z/research/market-clusters.html
  - https://mark-c4r.github.io/Jay-Z/research/growth-opportunities.html
  - https://mark-c4r.github.io/Jay-Z/research/seo-recipes.html
  - https://mark-c4r.github.io/Jay-Z/research/ten-year-picture.html
  - https://mark-c4r.github.io/Jay-Z/practical/
- Before/after screenshots archived
- Jarda informed via WhatsApp
- Retro committed

### Verification commands

```bash
# Slice 1 — YouTube chapter accessibility
yt-dlp --no-download --skip-download --print "%(chapters)j" "https://youtu.be/z9rdrNrkvDY"
yt-dlp --no-download --skip-download --print "%(chapters)j" "https://youtu.be/cNf7uVff11Y"
yt-dlp --no-download --skip-download --print "%(chapters)j" "https://youtu.be/yiJOTCRVWjc"
yt-dlp --no-download --skip-download --print "%(chapters)j" "https://youtu.be/aFQskhdR3RQ"

# Slice 3/4/5 — local preview
cd /Users/profile_1/Coding/jarda/jarda-ai-start && python3 -m http.server 8000
# open http://localhost:8000/ and click through

# Slice 6 — cross-model dispatch (exact commands finalized per project-orchestrator conventions)
#   codex … plan-review on <reshape-draft bundle>
#   gemini … UI-review on <reshape-draft bundle>

# Slice 7 — deploy verification
curl -sI https://mark-c4r.github.io/Jay-Z/ | head -1
curl -sI https://mark-c4r.github.io/Jay-Z/research/market-clusters.html | head -1
curl -sI https://mark-c4r.github.io/Jay-Z/research/growth-opportunities.html | head -1
curl -sI https://mark-c4r.github.io/Jay-Z/research/seo-recipes.html | head -1
curl -sI https://mark-c4r.github.io/Jay-Z/research/ten-year-picture.html | head -1
curl -sI https://mark-c4r.github.io/Jay-Z/practical/ | head -1
```

## Deferred items (stay deferred unless feedback escalates)

From `UNFINISHED-WORK.md`:
- **v1.5 features:** Market Intel deeper than C7.4, SEO deep-dive beyond C7.7, Video Cards richer than chapter lists, Practitioners sidebar — ALL remain deferred. Reshape redistributes current research content but does not deepen it.
- **v2 interview protocol phases 4–6** — remain deferred. Phases 1–3 covered design; 4–6 were contingency.
- **Customization-ack (C7.2) reconsideration** — folded: "Jay-Z" persona is upgraded to a first-person owner voice in the intro ("these are notes I put together for you") rather than placeholder-slot acknowledgment.
- **Single-vector deep-dive research** (if Jarda responds to a specific brief finding — e.g. SEO, YouTube, travel editorial) — stays deferred by design. The humility clause in §4 invites him to pick a vector; if he does, THAT is the next engagement, not v1.

## Open items for shape phase (resolve during Slice 1–2)

- **Structure decision** (single-page progressive vs main + sibling pages) — decide in Slice 2 from Spike A + Spike B + Spike C findings. N=1 personal-brief patterns win conflicts with N≥10 e-learning / exec-summary norms. Provisional layout in "Candidate site structure" above is not a commitment.
- **Section ordering** — Slice 2 tests canonical (§1 intro → §2 AI → §3 Cowork → §4 brief → §5 practice → §6 appendix) vs teaser-forward (§1 intro → §2 brief teaser → §3 AI → §4 Cowork → §5 full brief → §6 practice → §7 appendix). Pick one with documented rationale against identity→action compass.
- **Vocabulary** ("Section" vs "Lesson" vs "Part" vs alternative) — decide from Spike A, filtered through Spike C.
- **Voice posture** — 1-paragraph voice guidance + 2–3 "sounds like / doesn't sound like" sample pairs (~50 words each) written in Slice 2 from Spike C + voice-audit findings. Anchor: "Mark writing to one friend over WhatsApp."
- **Opening-90-seconds contract** (Slice 2 acceptance criterion, NON-NEGOTIABLE) — §1 intro must answer (a) who + why naming Mark, (b) what this is for Jarda specifically, (c) one immediate payoff teaser. Draft ~150 words committed with blueprint.
- **Exec-summary brief outline** — sub-section list + word budget — decided in Slice 2 from Spike B filtered through Spike C.
- **Humility clause wording + position — two placements** — top of §4 (1 sentence surface-level framing) + end of §4 (2 sentences deep-dive invitation). Both drafted in Slice 2.
- **Go Deeper audit criterion** — upgrade to "would Jarda click this?" (N=1 test). Expect >80% kill rate, not prune-to-1-per-section (N-reader taste). Survivors documented with per-branch reason in Slice 2.
- **Master-section titles + timestamps** per video — finalized in Slice 1 source-rescan; interview-group titles weight stand-alone concept naming, learning-group lean memory-trigger; locked in Slice 2.
- **Business brief content** (§4) — drafted in Slice 5 from the 24 unshipped research docs, following Slice 2 outline + word budget. MUST include 1–2 Jarda-specific references (WhatsApp phrase, site URL, business-specific line); escalate if zero pullable.
- **Guided-practice prompts** (§5) — 4–6 paste-ready prompts drafted in Slice 5, anchored to brief findings + video concepts. At least one references Jarda-specific business detail (no generic "[your business]" placeholders).
