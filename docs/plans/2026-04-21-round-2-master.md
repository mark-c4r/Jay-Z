---
ticket: jarda-ai-start#round2-master
status: completed
appetite: M (7 cluster sections, Path B+ Hybrid)
project: jarda-ai-start
updated: 2026-04-21
supersedes: 2026-04-21-cluster-1-market-map-correction.md, 2026-04-21-cluster-2-bug-sweep.md, 2026-04-21-cluster-3-prerequisites.md, 2026-04-21-cluster-4-design-ia.md, 2026-04-21-cluster-5-youtube-chapters.md, 2026-04-21-cluster-6-appendix-depth.md
files: [index.html, docs/design/2026-04-21-c4a/*]
---

# Round 2 Master Shape — Jarda AI-Start Remediation

ONE master shape doc covering all 7 refactored clusters (C1, C2, C3, C4a, C4b, C5, C6). Each section is a self-contained Shape-Up contract: Problem, Verified Assumptions, Shape, Acceptance Criteria, Slices, No-Gos, Verify commands.

**Path B+ Hybrid execution:** one doc, MANDATORY Codex R2 on the 4 risk-≥4 sections (C2, C3, C4a, C5), S/low-risk builds can run in parallel with Codex R2 on heavier ones.

---

## 0 · Status & approach

**State:** v2b shipped to `mark-c4r/Jay-Z` at `cf3e0a6` (clean). Round 1 produced 6 shape contracts (kept as reference at `docs/plans/2026-04-21-cluster-*.md`) → Codex R1 returned 4 REJECTs + 2 APPROVE_WITH_REV → 3 UX streams (Chief UX + common-Qs + Gemini v2) surfaced convergent findings → 5 open decisions now resolved (see prior HANDOFF). This doc folds all three input streams into 7 actionable contracts.

**Build ceiling:** Once user approves this master shape, scope is LOCKED per section. Additions require re-shaping that section. Scope can always be CUT via circuit breaker.

**Why one master doc instead of 7 separate:** Codex R1 + 3 UX streams already reduced unknowns substantially. The cost of 7 parallel shape subagents + 6 more Codex review rounds doesn't pay off when the cluster boundaries are well-understood. One doc keeps cross-cluster consistency (voice, AC style, invariants) and reduces review surface.

---

## 1 · Locked invariants (apply to every cluster)

### Voice

- **Register:** "friend-from-highschool" — never "expert / vendor / thought-leader"
- **Never:** "You must", "The secret to", "Game-changing", "Revolutionary", "AI will change everything"
- **Prefer:** "Here's how I do it", "This part sucks, but do it anyway", "What surprised me", "Don't skip this"
- **Sobriety rule:** if a sentence could appear in a product-launch tweet, rewrite it

### Privacy (revised 2026-04-21 post-consultation)

**Model:** "Jay Z placeholder + descriptive" — keep placeholder persona name; describe reader's business context without linking his own URLs; name real competitors WITH their public URLs (they're public businesses, fair game); add `<meta name="robots" content="noindex,nofollow">` to prevent search-engine indexing as a safety net.

**Ship:**
- ✅ `Jay Z` placeholder stays as reader's name in the primer
- ✅ Describe reader's business niches (adventure-elopement photography, CZ travel-book author, Scandinavian peak guide) without linking his URLs
- ✅ Name real competitors with their public URLs (2 Brides, Ceranna Photography, Tanja Ferm, Ladislav Zibura, Honest Guide, Ben Love, etc.) — already public businesses
- ✅ Professional voice about competitors — honest assessment, no trash talk

**Never ship:**
- ❌ Real name "Jarda" / "Jarda Zaoral" (first or last) — no proper-noun exposure in public page
- ❌ Reader's own URLs: `thebestviewpoints.com`, `korunaevropy.cz`, `jardaphoto.*`, Instagram/podcast handles
- ❌ Referral codes, API keys, credentials, banking — standard sensitive patterns
- ❌ Any content not already public about reader or competitors

**Audit gate: DISABLED for this primer** (per user decision 2026-04-21). The `scripts/privacy-audit.sh` file stays in umbrella for future projects, but is NOT a required gate on builds/commits/pushes in this repo. Manual review replaces the gate. Grep-based spot-checks documented in each cluster's Verify section.

**Rotation rule (unchanged):** if a secret hits git history, rotate — don't try to rewrite history.

### Style

- Design tokens (do NOT invent): `--bg`, `--ink`, `--muted`, `--accent`, `--bg-inset`, `--focus-ring`, `--rule-soft`, `--rule`
- No dependencies, no build step, no backend, no analytics, no framework
- Single file: `jarda-ai-start/index.html` (2171 lines, ~116KB at `cf3e0a6`)
- localStorage schema v4 (fresh state on load, no migration)
- Print stylesheet exists at line 946 — reuse for any save-page feature
- Diagrams: hand-styled SVG in `assets/diagrams/` (v2b shipped 6 new diagrams)

### Lifecycle

- 30-day take-down window (or reader says "I've got what I need")
- Before take-down: capture to vault alongside other shipped projects

---

## 2 · Cluster map & dispatch

| Cluster | Appetite | Risk | MANDATORY Codex R2? | Blocks | Can run in parallel with | Primary file |
|---|---|---|---|---|---|---|
| C1 Teaching-voices block (replaces Market map) | S | 1 | no (optional) | none | any | `index.html:1812-1836` (appendix block rename + content swap) |
| C2 Bug sweep + if-stuck cure | M | 4 | **YES** | nothing | C1/C4b/C6 | `index.html:1282-1290, 1525-1535, activateFacade` |
| C3 Before-you-begin cure (wide) + customization-acknowledgment line | M-L | 5-6 | **YES** (double-priority) | C4a masthead (mutually informing); C7 (shared intro line) | C1/C4b/C6 (non-overlapping) | `index.html:1304, 1348, 1529, try-one blocks` |
| C4a Structural (masthead/TOC/save/for-devs label) | M | 4 | **YES** | requires visual reference artifact at `docs/design/2026-04-21-c4a/` | C3 coordination needed | `index.html:1040-1060, 1282-1290, 1343, completion reveal` |
| C4b Voice softening sweep | S-M | 2-3 | no (optional) | none | C1/C6/C7 | `index.html:1529, 1594, 1737` |
| C5 YouTube chapters | M | 4 | **YES** | nothing | C1/C4b/C6/C7 | `index.html:1314-1730 (7 facades), activateFacade JS` |
| C6 Appendix voice tightening + redirects | S | 2 | no (optional) | C3 delivers 11GB cure into Stop 4; C7 expands appendix | C1/C4b/C7 | `index.html:1787-1843 (appendix), 1725-1770 (Stop 6)` |
| C7 Business-aware appendix (Jarda-specific) + noindex | M | 3-4 | **recommended** (new competitor-naming surface) | None, but shares intro line with C3 | C4b/C5 | `index.html:<head>, 1787-1843 (appendix expansion)` |

**Build-order recommendation (dispatch sequence):**

```
Day 1 — locked
├─ C1 ────── S, ship fast (voice signal lands quickly)
├─ C4b ───── S-M, ship fast (voice signal lands quickly)
├─ C6 ────── S, ship fast (voice polish on existing blocks)
├─ C7.1 ──── noindex meta tag (2 min, ship immediately)
└─ Codex R2 dispatched in parallel on C2, C3, C4a, C5, C7 drafts

Day 2 — after Codex R2
├─ C4a ────── has visual reference artifact → build
├─ C3 ─────── build after C4a masthead settles (shares intro line with C7)
└─ C2 ──────── build after C3 (IO scroll-sync depends on final masthead geometry)

Day 3 — after C3/C4a
├─ C5 ──────── chapter rendering under the stable facade
└─ C7 (main) build remaining appendix blocks (D/E/F) — longest content writeup
```

---

# C1 · Teaching-voices block (replaces Market map)

**Appetite:** S · **Risk:** 1 · **Codex R2:** optional (skip recommended)

## Problem

Appendix block 2 currently labeled "Market map" with 6 names (Hesselberg, Ceranna, Zibura, Ben Love, Honest Guide, Rexby) — **these are the reader's BUSINESS COMPETITORS from `discovery-plan.md`, not AI teachers.** A prior session pasted the competitive-landscape names into the appendix mislabeled as "other voices teaching in this space". This is a content error.

**Two problems at once:**
1. The block has the wrong CONTENT (competitors masquerading as teachers) — user's "Ruben Hassid, Sarah Cordiner — idk who are these" question surfaced the confusion
2. The block has the wrong LABEL — "Market map" is actually what the NEW C7 competitive landscape block will be; this block should become "Teaching voices" with real AI-teachers content

**Resolution:**
- Rename block to "Teaching voices" (or similar — "Who to follow next", "Voices around Cowork")
- Replace 6 competitor names with 3 AI teachers confirmed by user: **Ruben Hassid + Jeff Su + Jesse Genet**
- The 6 competitor names move to C7 Block D "Competitive landscape" where they belong
- No voice prefix (Codex R1 preempted-decision resolved: DROP)

## Verified Assumptions

| Claim | Source of truth | Verify |
|---|---|---|
| Appendix block 2 currently labeled "Market map" with 6 names | `index.html:1812-1836` at `cf3e0a6` | rg -n "Market map" jarda-ai-start/index.html |
| 6 names present: Hesselberg, Ceranna, Zibura, Ben Love, Honest Guide, Rexby | `index.html` at `cf3e0a6` | rg -n "Hesselberg\|Ceranna\|Zibura\|Ben Love\|Honest Guide\|Rexby" jarda-ai-start/index.html |
| These 6 are reader's business competitors, not AI teachers | `/Users/profile_1/Coding/jarda/discovery-plan.md:52-77` (Competitive landscape) | sed -n '52,77p' /Users/profile_1/Coding/jarda/discovery-plan.md |
| Ruben Hassid is a real AI teacher with Cowork curriculum | discovery-plan.md:252 | rg -n "Ruben Hassid" /Users/profile_1/Coding/jarda/discovery-plan.md |
| Jeff Su (discovery-plan.md:256) + Jesse Genet (discovery-plan.md:254) confirmed | discovery-plan.md | rg -n "Jeff Su\|Jesse Genet" /Users/profile_1/Coding/jarda/discovery-plan.md |
| No voice-prefix ("Friend/Expert/Peer") currently exists | `index.html` at `cf3e0a6` | rg -n "Friend:\|Expert:\|Peer:" jarda-ai-start/index.html → no matches |

## Shape

Block 2 of appendix renamed + replaced:

**New block title:** "Teaching voices" (alternatives: "Who to follow next", "Voices around Cowork")

**New content (3 voices, no prefix):**

- **Ruben Hassid** — [*How to AI* Substack](https://ruben.substack.com/). The clearest non-technical Claude Cowork curriculum online. Coined the progression *prompts → projects → skills* that matches the shape of this primer. April 2026 Skills guide is the reference practitioners share. Best standalone starting point if the reader wants a second voice.
- **Jeff Su** — [jeffsu.org](https://www.jeffsu.org/). Productivity/workflow creator. The Stop 1 video is his. Low-fluff, high-signal. If the reader liked Stop 1's pacing, there's more like it.
- **Jesse Genet** — [Lenny's Newsletter write-up](https://www.lennysnewsletter.com/p/5-openclaw-agents-run-my-home-finances) + [a16z video](https://www.youtube.com/watch?v=yiJOTCRVWjc). Non-technical parent running agents at home; already featured in Stops 5-6. The habits (voice-first, confetti time, Obsidian 2nd brain) transfer to the reader's life even though the stack differs.

Keep the 3 short "observations" paragraphs after the list but rewrite them for 3 voices instead of 6. (Observations about splits along axes, learning-by-recording, non-vendor incentives — still apply.)

Jack Roberts is intentionally NOT in this block because he's already the centerpiece of Stop 4 facade; listing him here is redundant (confirmed: user choice).

## Acceptance Criteria (block-local)

- [ ] Block 2 heading renamed from "Market map" to "Teaching voices" (or similar agreed phrase)
- [ ] Block lists exactly 3 voices: Ruben Hassid, Jeff Su, Jesse Genet (all 3 with URLs)
- [ ] None of {Hesselberg, Ceranna, Zibura, Ben Love, Honest Guide, Rexby} appear in Block 2 (they migrate to C7 Block D)
- [ ] Observations paragraphs updated for 3-voice list (not 6)
- [ ] No prefix ceremony ("Friend/Expert/Peer" or similar)
- [ ] Ruben Hassid's Substack URL is live and points to current content (link-check)
- [ ] Voice register matches existing appendix blocks

## Slices

- **C1.1** — rename block 2 heading, replace `<ul>` content with 3-voice list + URLs, rewrite observations for 3 voices (~30 min)

## No-Gos

- No voice-prefix framing
- No 4th voice in this block (3 is the Gemini overwhelm-signal answer)
- No verdict language about the 3 teachers ("the best", "the definitive") — register stays honest/descriptive
- No links to Ruben's paid content (Substack free-tier only)
- No claim that appears evaluative ("must-read", "game-changing")
- Don't yet migrate the 6 competitor names to C7 — C7 section handles that independently (coordination noted, not code-coupled)

## Verify

```bash
# Before build
rg -n "Market map" jarda-ai-start/index.html
rg -n "Hesselberg|Ceranna|Zibura|Ben Love|Honest Guide|Rexby" jarda-ai-start/index.html
# After build
rg -c "Teaching voices|Who to follow|Voices around" jarda-ai-start/index.html  # expect 1 (heading)
rg -c "Ruben Hassid" jarda-ai-start/index.html  # expect 1
rg -c "jeffsu.org" jarda-ai-start/index.html  # expect 1
rg -c "lennysnewsletter" jarda-ai-start/index.html  # expect 1
# C1 alone does NOT remove competitor names (C7 Block D handles that); but block 2 should have them gone
rg -B2 "Ruben Hassid" jarda-ai-start/index.html  # should show block 2 heading just above
# Voice invariant
rg -n "Friend:|Expert:|Peer:|Watch:|Read:|Skip:" jarda-ai-start/index.html  # expect 0
```

---

# C2 · Bug sweep + if-stuck cure [MANDATORY Codex R2]

**Appetite:** M · **Risk:** 4 · **Codex R2:** MANDATORY

## Problem

Post-Codex R2 rescope (dropped Bug #3 hamburger claim as unverified; scoped #tb-fill out of conflict):

1. **Bug #1 — topbar stop indicator doesn't scroll-sync.** As the reader scrolls through Stop 1 → 6, the topbar's "Stop X of 6" indicator (`#tb-stop`) and title (`#tb-title`) stay frozen on whatever was last clicked. This signals the page isn't tracking them. **Scope note:** fix `#tb-stop` + `#tb-title` only; DO NOT change `#tb-fill` semantics (see No-Go §6 below).
2. **Bug #2 — click-to-jump broken on mobile.** The existing click-to-jump on YouTube facades (click facade → iframe bootstraps + seeks) works on desktop but the touch handler chain fails on iOS Safari / Android Chrome.
3. ~~**Bug #3 — hamburger does nothing.**~~ **Removed.** Codex R2 P0.1 flagged this as a false diagnosis. Grep-verified at `cf3e0a6`: a full working drawer exists (`menuToggle.addEventListener` at line 2030, `openDrawer`/`closeDrawer` at 1983-2005, focus trap, escape key close, backdrop click close, auto-close on rail-link navigation). If the reader later reports a specific runtime failure (viewport, browser, state), spin a separate small bug ticket with the repro.
4. **Cure #1 (Chief UX + Gemini convergence):** "Stuck?" fallback. Two-layer: (a) inline one-liner at Stop 4 main block (the connector stop, highest confusion density) teaching reader to ask Cowork itself via screenshot; (b) email-Mark footer fallback.
5. **Cure #2 (Codex R1 P1):** IntersectionObserver has no fallback for older browsers. Use a `scroll` event + `getBoundingClientRect` path when `window.IntersectionObserver` is undefined.

## Verified Assumptions

| Claim | Source | Verify |
|---|---|---|
| Topbar contains `#tb-stop`, `#tb-title`, `#tb-fill`, `#tb-block` spans | `index.html:1282-1286` | rg -n "tb-stop\|tb-title\|tb-fill\|tb-block" jarda-ai-start/index.html |
| `#tb-fill` currently driven by `state.completed.blocks` via `updateTopbar()` — this is block-completion UI, NOT scroll-position UI | `index.html:1940-1968` | sed -n '1940,1968p' jarda-ai-start/index.html \| rg "fill\|completed" |
| Working hamburger drawer already exists: `menuToggle.addEventListener('click', ...)` wired to `openDrawer`/`closeDrawer` state machine | `index.html:2030, 1983-2005` | rg -n "menuToggle\.addEventListener\|function openDrawer\|function closeDrawer" jarda-ai-start/index.html |
| IntersectionObserver is NOT currently used in the page | `index.html` at `cf3e0a6` | rg -c "IntersectionObserver" jarda-ai-start/index.html → expect 0 |
| **Existing facade activation signature is `activateFacade(facade)` — ONE parameter only** (Codex R2 P0 fix; was wrongly claimed as `activateFacade(facade, startOverride)` in earlier draft) | `index.html:2057` | rg -n "function activateFacade" jarda-ai-start/index.html → 1 match `function activateFacade(facade) {` |
| Existing facade callers pass only `facade` (no startOverride anywhere) | `index.html:2054, 2078` | rg -n "activateFacade(" jarda-ai-start/index.html |
| Stop 4 section starts at line 1525 (not 1529 as earlier claimed) | `index.html:1525` | rg -n 'id="stop-4"' jarda-ai-start/index.html → line 1525 |
| No existing "Stuck?" copy present | `index.html` at `cf3e0a6` | rg -ni "stuck\?" jarda-ai-start/index.html → 0 copy matches |

## Shape

- **Scroll-sync (narrow scope):** IntersectionObserver with 40% threshold watches each `.stop` section. On intersection, update **only** `#tb-stop` and `#tb-title`. `#tb-fill` stays unchanged (it's block-completion UI, not scroll-position UI). Block-tracking (`#tb-block`) stays driven by existing block-intersection logic (unchanged). Fallback: a passive `scroll` listener using `getBoundingClientRect()` guarded by `if (typeof IntersectionObserver === 'undefined')`.
- **Click-to-jump on mobile:** review the facade click handler at `index.html:2054`. The current handler is `facade.addEventListener('click', () => activateFacade(facade))`. If iOS Safari / Android Chrome touch-chain drops the click, add a `touchend` handler alongside (not replacing; click still fires after touchend). Prevent double-activation via an idempotent guard in `activateFacade` itself (e.g., early-return if iframe already active).
- **Hamburger:** NO CHANGES. The drawer already works (grep-verified, see VA). If a specific mobile bug surfaces later, file a separate small ticket with repro details.
- **"Stuck?" cure layer 1:** one inline sentence at end of Stop 4's MAIN rationale block (not the branch drawers). Placement anchor: the paragraph immediately before the first `<button class="chip" data-branch=...>` button in `#stop-4` Block 1. Copy: *"Stuck? Screenshot this stop and ask Claude: 'I'm at Stop 4 and I don't see the connector menu — help?' Cowork can read the page back to you."*
- **"Stuck?" cure layer 2:** one line inside `<footer>` element (grep-confirm existence during build). Copy: *"Stuck? Reply to the email I sent you with this link — I'll help unstick."*

## Acceptance Criteria (block-local)

- [ ] Scroll from Stop 1 to Stop 6 on desktop: `#tb-stop` text updates to current stop index within 500ms of crossing 40% visibility threshold of the new stop. Same on mobile (375px viewport).
- [ ] `#tb-title` updates in sync with `#tb-stop`.
- [ ] `#tb-fill` unchanged: still driven by `state.completed.blocks` via `updateTopbar()`. Verify: pre-fold and post-fold `#tb-fill` width behavior is identical (run through completing 1-2 blocks; confirm same width output).
- [ ] In an environment where `window.IntersectionObserver` is undefined, scroll-sync falls back to `scroll` event + `getBoundingClientRect()` and still updates `#tb-stop` + `#tb-title` correctly.
- [ ] Tap any of the 7 YouTube facades on iPhone Safari (real device or simulator) → iframe bootstraps, seeks to correct `data-start`, autoplays.
- [ ] No changes to `#menu-toggle` / drawer behavior: `menuToggle.addEventListener('click', ...)` at line 2030 still fires; `openDrawer`/`closeDrawer` state machine unchanged.
- [ ] Stop 4 MAIN block (inside `<section id="stop-4">`, before the first branch-drawer `<button class="chip">`) contains the "Stuck?" screenshot-ask sentence. Verify: `sed -n '/id="stop-4"/,/class="chip" data-branch="stop-4/p' index.html | grep -c "Stuck? Screenshot"` → expect 1.
- [ ] `<footer>` element contains the "Reply to the email" fallback. Verify: `sed -n '/<footer/,/<\/footer>/p' index.html | grep -c "Reply to the email"` → expect 1.
- [ ] No regressions: all 7 facades still activate (grep `class="yt-facade"` → expect 7), completion-reveal `hidden` attribute + reveal behavior preserved, `state` schema v4 unchanged.
- [ ] Early-return guard added to `activateFacade(facade)` so double-fires don't double-instantiate iframes.

## Slices

- **C2.1** — IntersectionObserver scroll-sync for `#tb-stop` + `#tb-title` ONLY + pre-IO fallback (~45 min)
- **C2.2** — Touch-click-to-jump fix + idempotent-guard in `activateFacade` (~40 min)
- **C2.3** — "Stuck?" Stop 4 MAIN block cure (anchored placement) (~15 min)
- **C2.4** — "Stuck?" footer fallback copy (anchored placement) (~10 min)

## No-Gos

- **No changes to `#tb-fill`.** It stays block-completion UI. Do not repurpose it for scroll position. (Codex R2 P0.2 fix.)
- **No changes to the hamburger / drawer.** It works. Do not remove, do not re-implement. (Codex R2 P0.1 fix.)
- No replacement of facade JS with `<iframe>` eager-load
- No new dependencies (no IntersectionObserver polyfill; use the scroll+getBoundingClientRect fallback)
- No topbar structural/visual redesign (only IO wiring + two text updates)
- No Cowork API call or actual AI integration in "Stuck?" — it's just copy that teaches the pattern
- No modification of Stop 4 branch drawers, only the main block (preserves C3.c 11GB cure placement)
- The `activateFacade` signature MAY be extended to `activateFacade(facade, startOverride)` but only as needed by C5 (coordinate with C5 during build — if C5 ships first, C2 uses the extended signature; if C2 ships first, keep 1-param)

## Verify

```bash
# Before build
rg -c "IntersectionObserver" jarda-ai-start/index.html
# After build: should show new IO logic
# Stop 4 Stuck? sentence
rg -n "Stuck\? Screenshot" jarda-ai-start/index.html
# Footer fallback
rg -n "Reply to the email" jarda-ai-start/index.html
# Fallback path exists for pre-IO browsers
rg -n "getBoundingClientRect" jarda-ai-start/index.html
```

---

# C3 · Before-you-begin cure (wide) [MANDATORY Codex R2 — double priority]

**Appetite:** M-L · **Risk:** 5-6 · **Codex R2:** MANDATORY (double: risk + user-facing framing irreversibility)

## Problem

Cold-start bounce is the single biggest gap per all 3 UX streams. The page currently goes straight to Stop 1 rationale with no identity, no duration, no "what this is", no mobile reality check, no vocabulary flattener (Chat vs. Cowork vs. Code), no prerequisites, no safety context (the 11GB delete incident is everywhere in public discourse). Additionally: the try-one block preamble ("Do NOT save, create, move, or edit any file until I review and approve.") is repeated 6 times across the stops, which Chief UX flagged as boilerplate-fatigue.

**Absorbs from round 1:** the C3 "Prerequisites" cluster (which Codex R1 REJECTED for being too narrow).

**Absorbs from UX streams:**
- Chief UX item #1 (identity/time-cost cure)
- Chief UX item #2 (runner-framing consolidation)
- Chief UX item #5 (one-card prereq above Stop 1)
- Common-Qs #1 (Chat/Cowork/Code flattener)
- Common-Qs #2 (Pro/free/Max sidestep via "what you need")
- Common-Qs #3 (implied install)
- Common-Qs #4 (11GB safety cure into Stop 4)
- Gemini #1-2 (mobile app vs. web + local folder on iPhone)

## Verified Assumptions

| Claim | Source | Verify |
|---|---|---|
| Stop 1 opens at `<section id="stop-1">` on line 1304 | `index.html:1304` | rg -n 'id="stop-1"' jarda-ai-start/index.html |
| Nothing exists between `<main>` opener and Stop 1 currently | `index.html:1300-1304` | sed -n '1296,1306p' jarda-ai-start/index.html |
| "Do NOT save" appears exactly 6 times | `index.html` at `cf3e0a6` | rg -c "Do NOT save" jarda-ai-start/index.html → 6 |
| No existing "prerequisites" / "before-you-begin" / byline / duration-badge UI | `index.html` at `cf3e0a6` | rg -n -i "prerequisites\|before.you.begin\|by mark\|~20 min\|estimated" jarda-ai-start/index.html → no copy matches |
| Cowork is Mac/Windows-only today (mobile uses Dispatch or Claude mobile app for read-only) | Anthropic public docs + common-Qs research last 30d | (external — confirm at Slice 1 via WebFetch if any doubt) |
| Stop 4 rationale on line 1529 contains "Nothing is hidden" — the sentence to anchor the 11GB cure near | `index.html:1529` | rg -n "Nothing is hidden" jarda-ai-start/index.html |
| Stop 1 first try-one "Do NOT save" at line 1348 | `index.html:1348` | rg -n -B2 -A2 "First draft in chat. Do NOT save" jarda-ai-start/index.html |

## Shape

### 3.a — Prereq / identity card above Stop 1

One new card element between `<main>` and `<section id="stop-1">`. Six content slots:

1. **Byline** (1 line): *"A primer by Mark — friend, not vendor. Written for one reader."*
2. **Duration** (1 line): *"~20 minutes end to end. Skip anywhere — the rail saves your spot."*
3. **What this is** (1 line): *"Claude Cowork, explained as the tool itself: ChatGPT with memory, files, and a few connectors."*
4. **Mobile reality check** (2 lines): *"Cowork runs on desktop (Mac or Windows). On your phone, use the Claude mobile app — it reads your projects but can't do setup. Read this primer from wherever; do the setup at a keyboard."*
5. **Vocabulary flattener** (3 lines): *"Three names to untangle once. **Chat** — the conversation-only version (chatgpt-style). **Cowork** — chat plus projects, files, memory, connectors (this primer). **Code** — a terminal tool for developers. If you don't edit code for a living, Cowork is the one."*
6. **Prerequisites** (3 bullets, compact): *"Claude account (Pro recommended — $20/mo gets you Cowork). Desktop for setup. A notes app you already use (for your project's Instructions file)."*

Visual treatment: small card, `--bg-inset` background, `--rule-soft` border, `--accent` left border, ~120-180 words total. Sits above Stop 1 like a section lede. No new stop, no new heading level beyond `<h2>` (matches existing stop-title hierarchy).

### 3.b — Runner-framing consolidation

At Stop 1's first try-one block (line 1346-1355), add one framing line just above the `<pre class="try-one-prompt">`:

> *"These 'try-one' blocks are read-alongs. Paste into claude.ai if you're already signed in, or just read — the shape is what matters here."*

Then **strip the "Do NOT save, create, move, or edit any file until I review and approve" preamble from all 6 try-ones**. This safety framing moves into Stop 4 (connector stop), where write-access is the actual subject.

### 3.c — 11GB incident cure (inline at Stop 4)

Add one sentence to Stop 4's main rationale (after line 1529's "Nothing is hidden." or replacing that close):

> *"You've probably seen the viral story — someone said Claude deleted 11 GB of their files. Worth knowing why it's misleading: write access is off by default. If you never grant it, Cowork can only read and report back. Grant write per-surface, per-task."*

(This also serves the C4b voice-softening goal — replaces "Nothing is hidden." with honest context. Budget: ~2 sentences added, 1 sentence removed.)

## Acceptance Criteria (block-local)

- [ ] New prereq/identity card exists above `<section id="stop-1">` with 6 content slots as specified
- [ ] Stop count remains 6 (no Stop 0 created; `rg -c '<section id="stop-[0-9]"' index.html → 6`)
- [ ] Card is responsive (readable on 375px mobile)
- [ ] "Do NOT save" count: `rg -c "Do NOT save" index.html → 0` (or 1 if the safety framing moved intact into Stop 4)
- [ ] Stop 1 first try-one has the read-along framing line
- [ ] Stop 4 rationale contains 11GB cure (grep for "11 GB")
- [ ] "Nothing is hidden" removed (or softened — see C4b coordination)
- [ ] New card + rationale both pass voice audit (no "Revolutionary", "Game-changing", "You must"; register matches existing stops)
- [ ] privacy audit green: `bash /Users/profile_1/Coding/jarda/scripts/privacy-audit.sh jarda-ai-start/` exits 0
- [ ] Lighthouse a11y ≥ 0.95 (baseline was 1.0)

## Slices

- **C3.1** — prereq/identity card markup + CSS (~60 min)
- **C3.2** — runner-framing consolidation: strip 5 preambles, add 1 framing line at Stop 1 (~30 min)
- **C3.3** — Stop 4 11GB cure sentence + "Nothing is hidden" soften (~20 min)
- **C3.4** — verification pass (voice audit, Lighthouse, responsive check) (~30 min)

## No-Gos

- No new stops. Stop count stays at 6.
- No full "Stop 0 / Before you begin" heading or section
- No new drawer / branch pattern inside the prereq card
- No claims about Anthropic pricing that may drift (reference "Pro" without quoting exact price beyond the one-time $20 in the prereq card; ok to drop the $20 if preferred)
- No new Pro-vs-Free advice beyond "Pro recommended"
- No addressing the "11GB" issue outside Stop 4 (don't add warnings to Stop 1 or the prereq card about deletion risk — wrong framing, wrong place)

## Verify

```bash
# State before
rg -c "Do NOT save" jarda-ai-start/index.html  # expect 6
rg -n "id=\"stop-0\"" jarda-ai-start/index.html  # expect no match
# After build
rg -c "<section id=\"stop-" jarda-ai-start/index.html  # expect 6
rg -n "11 GB\|11GB" jarda-ai-start/index.html  # expect 1+ match in Stop 4
rg -n "read-along" jarda-ai-start/index.html  # expect 1 match at Stop 1
rg -n "A primer by Mark" jarda-ai-start/index.html  # or current byline wording, expect 1 match
bash /Users/profile_1/Coding/jarda/scripts/privacy-audit.sh jarda-ai-start/
```

---

# C4a · Structural — masthead, TOC, save-page, for-devs label [MANDATORY Codex R2]

**Appetite:** M · **Risk:** 4 · **Codex R2:** MANDATORY · **BLOCKS ON:** visual reference artifact at `docs/design/2026-04-21-c4a/` committed before build

## Problem

- Current "masthead" is just the utility topbar (line 1282) — no identity, no duration, nothing to anchor a returning reader. Chief UX top-1 issue.
- No TOC jump affordance other than the left rail (which is invisible on narrow screens unless the hamburger works — see C2).
- No save-page button. Reader who wants to preserve the primer has to know `Cmd+P` → Save as PDF. Chief UX top-4 issue.
- Stop 1 diagram alt text already says "Code (developer-grade CLI + IDE)" and "Codex (autonomous agent, CLI-based)" — but the VISUAL SVG doesn't label these columns as "for developers only" — Gemini recommendation.

Coordination with C3: the prereq/identity card (C3.a) conveys similar identity signal. C4a's masthead should be complementary, not redundant — the masthead lives in the topbar (always visible), the prereq card lives above Stop 1 (only visible at the start). Decide at shape review how much byline/duration content sits in each.

## Verified Assumptions

| Claim | Source | Verify |
|---|---|---|
| Existing topbar is `<header class="topbar">` at line 1282 | `index.html:1282-1290` | rg -n 'class="topbar"' jarda-ai-start/index.html |
| Print stylesheet exists at line 946 | `index.html:946` | rg -n "@media print" jarda-ai-start/index.html |
| Completion reveal is at `<section class="completion-reveal" id="completion-reveal">` around line 1785 | `index.html:1785-1797` | rg -n 'id="completion-reveal"' jarda-ai-start/index.html |
| No existing save-page button | `index.html` at `cf3e0a6` | rg -n -i "save.*page\|print.*button\|window\.print" jarda-ai-start/index.html → no button code |
| Stop 1 diagram SVG is `assets/diagrams/stop-1-positioning.svg` | `index.html:1343` | rg -n "stop-1-positioning.svg" jarda-ai-start/index.html |
| Left rail exists as TOC substitute | `index.html` at `cf3e0a6` | rg -n 'id="rail"' jarda-ai-start/index.html |

## Shape

### 4a.1 — Masthead enrichment (in topbar)

Minimal add to existing `.topbar` structure. Add 2 new elements:
- **Byline chip** (left of existing "Stop X of 6"): small text *"A primer by Mark"* — links to a `#about` anchor in the research appendix, or just static text.
- **Duration badge** (right of `.topbar-block`): small text *"~20 min"* — no click.

Both use existing tokens (`--muted`, `--ink`), sit inside `.topbar`, don't change its height, hide gracefully below 480px.

### 4a.2 — Save-page button

Button near completion reveal: *"Save this page"* → `window.print()`. Works because print stylesheet is already built. Add an inline tweak to ensure completion reveal state is printable (it's `hidden` until revealed — if reader prints before scrolling through, result is incomplete; add a note or conditionally expand).

### 4a.3 — Stop 1 diagram "For Developers Only" label

Edit `assets/diagrams/stop-1-positioning.svg` to add a subtle label over the Code + Codex columns: small text *"For developers"* in `.ink` color, positioned above or below the column labels. Keep the hand-drawn Excalidraw aesthetic (2px stroke, `#222` / `#a84b2b`). Update alt text accordingly.

### 4a.4 — Visual reference artifact (REQUIRED before build)

Per workflow.md and Codex R1 P0: commit the target mockup before build.

- Create `docs/design/2026-04-21-c4a/`
- `masthead-target.png` — desktop screenshot or annotated mockup of the enriched topbar
- `save-page-button.png` — screenshot of button placement near completion reveal
- `diagram-label.svg` or `.png` — target state for Stop 1 diagram with "For developers" label
- `tokens.md` — CSS-to-implementation table (any new tokens used? Likely none — reuse `--muted`, `--ink`)

Builder agent treats `docs/design/2026-04-21-c4a/` as acceptance criterion, not plan text.

## Acceptance Criteria (block-local)

- [ ] `docs/design/2026-04-21-c4a/` committed before C4a build starts (gate)
- [ ] `.topbar` has new byline chip + duration badge (both visible on desktop, gracefully hidden/reflowed below 480px)
- [ ] "Save this page" button exists near completion reveal, triggers `window.print()`
- [ ] Stop 1 diagram SVG has "For developers" label on Code/Codex columns
- [ ] Stop 1 diagram alt text updated to reflect the new label
- [ ] No new CSS tokens introduced
- [ ] No topbar height increase on desktop (measure before/after via `preview_inspect .topbar height`)
- [ ] Lighthouse a11y ≥ 0.95
- [ ] Visual reference artifact in `docs/design/2026-04-21-c4a/` matches shipped state

## Slices

- **C4a.0** (BLOCKS BUILD) — visual reference artifact in `docs/design/2026-04-21-c4a/` (~30 min)
- **C4a.1** — masthead enrichment (byline + duration in topbar) (~40 min)
- **C4a.2** — save-page button near completion + print-state fix (~30 min)
- **C4a.3** — Stop 1 diagram label edit + alt text (~30 min)

## No-Gos

- No sticky TOC below topbar (the left rail IS the TOC; Gemini agreed)
- No new framework, no new tokens
- No masthead growth beyond enriched topbar (no new hero section)
- No redesign of completion reveal for save-page (just add a button)
- No JS heavy-lift for print (the existing `@media print` handles it)

## Verify

```bash
# Gate
test -d jarda-ai-start/docs/design/2026-04-21-c4a
# After build
rg -n "A primer by Mark\|~20 min" jarda-ai-start/index.html  # expect 1+ match
rg -n "Save this page" jarda-ai-start/index.html  # expect 1 match
rg -n "window\.print" jarda-ai-start/index.html  # expect 1 match
# SVG check
grep -c "For developers" jarda-ai-start/assets/diagrams/stop-1-positioning.svg  # expect 1+ match
# A11y baseline
# (run Lighthouse manually via browser devtools; no automated command)
```

---

# C4b · Voice softening sweep

**Appetite:** S-M · **Risk:** 2-3 · **Codex R2:** optional (skip recommended; low risk)

## Problem

Gemini v2 and Chief UX flagged three phrases as voice-drift — expert/vendor register creeping in:

- **"Nothing is hidden"** at Stop 4 line 1529. Flagged as marketing register, not friend.
- **"operating manual"** at Stop 6 line 1737 (video highlight text — *"Give each agent an operating manual — how to work with you, what you like, what you don't."*). Flagged as corporate.
- **"Provisioning hands over keys"** at Stop 4 Deeper drawer line 1594. Dense + scary for a non-technical reader.

Honorable mention — time-formula repetition: stops 1, 2, 3, 4 all use "two minutes to X, five minutes to Y" or close variant. Chief UX flagged as boilerplate.

Coordination with C3.c: C3 removes "Nothing is hidden" as part of the 11GB cure. So C4b's remaining targets are "operating manual" and "provisioning hands over keys" + time-formula smoothing.

## Verified Assumptions

| Claim | Source | Verify |
|---|---|---|
| "Nothing is hidden." is at end of Stop 4 rationale line 1529 | `index.html:1529` | rg -n "Nothing is hidden" jarda-ai-start/index.html |
| "operating manual" appears in Stop 6 Jesse Genet highlight at line 1737 | `index.html:1737` | rg -n "operating manual" jarda-ai-start/index.html |
| "Provisioning hands over keys" is in Stop 4 Deeper drawer line 1594 | `index.html:1594` | rg -n "Provisioning hands over keys" jarda-ai-start/index.html |
| No other instances of these phrases elsewhere | `index.html` at `cf3e0a6` | rg -c "Nothing is hidden\|operating manual\|Provisioning" jarda-ai-start/index.html |

## Shape

Phrase-level 1:1 replacements. No added sentences, no scope creep.

- **"Nothing is hidden"** → handled by C3.c (removed + replaced with 11GB cure). No action in C4b.
- **"operating manual"** → *"working notes"* or *"a how-to for working with you"* (pick at build). Change ONLY in Stop 6 line 1737 highlight text. Ensure the YouTube timestamp link still points to the same `t=2590` segment (the quoted phrase is a paraphrase of what Jesse says in the clip; `operating manual` appeared to be a less-accurate transcription).
- **"Provisioning hands over keys"** → *"Granting write access means the agent can change things outside the chat"* or *"Turning on write access is a different decision from turning on read access"* (pick at build). Stop 4 Deeper drawer line 1594.
- **Time-formula repetition:** audit stops 1-4 for the "X minutes to understand, Y minutes to set up" pattern. Keep the phrasing at stop 1 (first introduction); vary or drop at stops 2-4. Replace with concrete per-stop phrasing (e.g., "One connector at a time — start with Gmail").

## Acceptance Criteria (block-local)

- [ ] `rg -c "operating manual" index.html → 0`
- [ ] `rg -c "Provisioning hands over keys" index.html → 0`
- [ ] Time-formula repetition reduced: count of `two minutes`/`five minutes` phrasings drops by ≥ 50%
- [ ] Jesse Genet Stop 6 highlight link `t=2590` still resolves to correct segment
- [ ] No added sentences (net word count change in touched blocks within ±20 words)
- [ ] Voice audit: new phrasings use friend-from-highschool register

## Slices

- **C4b.1** — Stop 4 Deeper drawer rewrite (~20 min)
- **C4b.2** — Stop 6 Jesse highlight rewrite (~15 min)
- **C4b.3** — Time-formula audit + variance (~20 min)

## No-Gos

- No added sentences
- No scope creep to other stops' rationales
- No changes to Stop 4 main rationale (C3.c handles that)
- No changes to YouTube timestamps
- No more than 3 distinct phrase changes

## Verify

```bash
# Before
rg -c "Nothing is hidden" jarda-ai-start/index.html
rg -c "operating manual" jarda-ai-start/index.html
rg -c "Provisioning hands over keys" jarda-ai-start/index.html
# After — all three should be 0 (Nothing is hidden via C3.c; others via C4b)
# Time formula smoothing
rg -c "two minutes.*five minutes\|two minutes to \|five minutes to" jarda-ai-start/index.html
```

---

# C5 · YouTube chapters [MANDATORY Codex R2]

**Appetite:** M · **Risk:** 4 · **Codex R2:** MANDATORY

## Problem

All 4 videos used in facades have published chapters (verified via yt-dlp; data persisted to `docs/research/2026-04-21-round-2-research/{video-id}.json`). Round 1 made this claim unverified; now verified. Goal: surface per-chapter click-to-jump as a small chapter list beneath each facade, so the reader can navigate a 20-min video instead of watching blindly from the segment start.

## Verified Assumptions

| Claim | Source | Verify |
|---|---|---|
| 4 unique video IDs in facades: z9rdrNrkvDY, cNf7uVff11Y, yiJOTCRVWjc, aFQskhdR3RQ | `index.html` facades | rg -oP 'data-video-id="\K[\w-]+' jarda-ai-start/index.html \| sort -u \| wc -l → 4 |
| z9rdrNrkvDY (Jeff Su) has 9 chapters; cNf7uVff11Y 46; yiJOTCRVWjc 8; aFQskhdR3RQ 19 | `docs/research/2026-04-21-round-2-research/{id}.json` | `for v in z9rdrNrkvDY cNf7uVff11Y yiJOTCRVWjc aFQskhdR3RQ; do python3 -c "import json; print('$v:', len(json.load(open('docs/research/2026-04-21-round-2-research/'+'$v'+'.json'))))"; done` |
| **Existing facade activation signature is `activateFacade(facade)` — ONE parameter only** (Codex R2 P0 fix) | `index.html:2057` | rg -n "function activateFacade" jarda-ai-start/index.html → 1 match `function activateFacade(facade) {` |
| Existing callers: `facade.addEventListener('click', () => activateFacade(facade))` at line 2054 + one call at 2078 — neither passes a startOverride | `index.html:2054, 2078` | rg -n "activateFacade(" jarda-ai-start/index.html |
| **Interval-overlap filter is REQUIRED** — "start-within-window" filter produces zero chapters for 3 of 7 facade windows | Computed against persisted chapter JSONs | See §7.a below — per-facade overlap counts verified |
| YouTube iframe API `postMessage` with `{event:'command', func:'seekTo', args:[t, true]}` is the standard seek-during-playback pattern; requires `enablejsapi=1` in iframe src | [YouTube IFrame Player API](https://developers.google.com/youtube/iframe_api_reference) | (external reference) |

### 7.a — Per-facade interval-overlap chapter counts (grep-verified)

Computed 2026-04-21 against persisted JSONs; include in this doc as a table so builder has ground-truth at build time:

| Facade window | Video | Chapters in window (interval-overlap) | start-within-window (the WRONG filter — zero for 3 facades) |
|---|---|---|---|
| 0:30 – 3:30 (30-210s) | z9rdrNrkvDY | **2** | 1 |
| 14:29 – 15:30 (869-930s) | z9rdrNrkvDY | **1** | **0** ❌ |
| 6:16 – 8:35 (376-515s) | z9rdrNrkvDY | **1** | **0** ❌ |
| 8:43 – 10:30 (523-630s) | z9rdrNrkvDY | **2** | 1 |
| 22:58 – 25:59 (1378-1559s) | cNf7uVff11Y | **3** | 2 |
| 13:53 – 16:30 (833-990s) | yiJOTCRVWjc | **1** | **0** ❌ |
| 40:09 – 43:30 (2409-2610s) | aFQskhdR3RQ | **3** | 2 |

Total chapters across 7 facades with overlap filter: **13**. With start-within-window filter: 6 (and 3 facades get zero). The overlap filter is the only correct choice. Regenerate this table via `python3 scripts/compute-facade-chapters.py` if facade windows change.

## Shape

Three layers:

1. **Data (normalization + filter explicit):**
   - Normalize persisted JSON: `start_time` → `start`, `end_time` → `end` (integer seconds), preserve `title`. This is an EXPLICIT build step, not an implicit cast.
   - Embed as JS constant `const videoChapters = { 'z9rdrNrkvDY': [{start:0, end:139, title:'...'}, ...], ... }` seeded from normalized JSONs.
   - **Interval-overlap filter** applied per facade at render time: include chapter `c` if `c.start < facadeEnd && c.end > facadeStart`. For chapters starting before `facadeStart`, clamp the seek-target to `facadeStart` (don't seek into pre-facade content).
2. **Render:** below each facade, render a `<ul class="video-chapters">` with chapter buttons: `<button data-seek="139" type="button">2:19 — Cowork: Essential Settings</button>`. Style: tight, muted text, small. Reserve layout space to prevent CLS.
3. **Interact:**
   - **Signature extension required.** Current `activateFacade(facade)` (1 param, line 2057) must be extended to `activateFacade(facade, startOverride)`. Default behavior preserved: if `startOverride` is undefined, fall back to `facade.dataset.start`. Non-breaking — existing callers at lines 2054 + 2078 still work.
   - If facade is still static (iframe not yet bootstrapped): clicking a chapter calls `activateFacade(facade, clampedChapterStart)` — uses the new signature.
   - If iframe is active (user already clicked facade): clicking a chapter posts `{event: 'command', func: 'seekTo', args: [clampedChapterStart, true]}` to the iframe via `iframe.contentWindow.postMessage(msg, 'https://www.youtube.com')`. Iframe src MUST include `enablejsapi=1`.

## Acceptance Criteria (block-local — scoped to each of the 7 facade blocks)

The 7 facade block IDs (grep-confirmed via `data-video-id` + `data-start` combinations):

1. Stop 1 Block 1 facade: `z9rdrNrkvDY` @ 30-210 (intro)
2. Stop 2 Block 1 facade: `z9rdrNrkvDY` @ 869-930 (projects)
3. Stop 3 Block 1 facade: `z9rdrNrkvDY` @ 376-515 (memory)
4. Stop 4 Block 1 facade: `z9rdrNrkvDY` @ 523-630 (connectors)
5. Stop 4 Block 1 facade: `cNf7uVff11Y` @ 1378-1559 (Jack Roberts)
6. Stop 5 Block 1 facade: `yiJOTCRVWjc` @ 833-990 (Jesse at home)
7. Stop 6 Block 1 facade: `aFQskhdR3RQ` @ 2409-2610 (Jesse codify)

Block-local AC:

- [ ] `videoChapters` JS constant contains exactly 4 video-ID keys (`z9rdrNrkvDY`, `cNf7uVff11Y`, `yiJOTCRVWjc`, `aFQskhdR3RQ`), each mapping to a normalized chapter array with `start` + `end` + `title`. Verify: `rg -n "const videoChapters" index.html` + `rg -o "'[A-Za-z0-9_-]+'" | wc -l` within the object → 4.
- [ ] Each of the 7 facade blocks renders a `<ul class="video-chapters">` adjacent to the facade element. Verify: `rg -c 'class="video-chapters"' index.html` → **7**.
- [ ] Interval-overlap filter applied at render — chapter count per facade matches the table in §7.a (total 13 across 7 facades). Verify by visual inspection OR `python3` check against rendered HTML.
- [ ] For chapters whose `start` is before `facadeStart`, the rendered `data-seek` attribute equals `facadeStart` (not the chapter's original start). Verify: spot-check the first facade whose interval-overlap table row shows "chapter start < facade start".
- [ ] `activateFacade` signature is `activateFacade(facade, startOverride)` with `startOverride` optional. Verify: `rg -n "function activateFacade" index.html` → 1 match matching new signature.
- [ ] Default facade click preserves existing behavior (seek to `data-start`). Verify: tapping facade without touching chapter list = iframe bootstraps at `data-start` (manual smoke per facade).
- [ ] Click chapter on a static facade → iframe bootstraps, seeks to `clampedChapterStart`, autoplays (manual smoke per facade).
- [ ] Click chapter on active facade → iframe seeks via postMessage (no reload). Verify: `rg -n "func.*seekTo\|postMessage" index.html` → ≥1 match.
- [ ] iframe src includes `enablejsapi=1`. Verify: `rg -n "enablejsapi=1" index.html` → ≥1 match.
- [ ] Chapter buttons are keyboard-accessible: `<button type="button">` + focus-visible styling + Enter/Space activate (manual smoke).
- [ ] No layout shift (CLS): chapter-list space reserved before activation. Visual verify: Lighthouse CLS < 0.05 before and after.
- [ ] No regressions to existing `.highlights-list a[data-seek]` behavior inside the same video blocks. Verify: `rg -c 'class="highlights' index.html` before/after fold = same.
- [ ] Lighthouse a11y ≥ 0.95 (baseline 1.0).

## Slices

- **C5.1** — Normalize 4 chapter JSONs (`start_time`/`end_time`→`start`/`end`), apply interval-overlap filter per facade window, embed as `videoChapters` JS constant with clamped `data-seek` for pre-facade chapters (~45 min)
- **C5.2** — Extend `activateFacade(facade)` → `activateFacade(facade, startOverride)` with default-to-`dataset.start` fallback. Non-breaking for existing callers at lines 2054 + 2078. (~30 min)
- **C5.3** — Render `<ul class="video-chapters">` markup + CSS for each of 7 facade blocks (~45 min)
- **C5.4** — Wire chapter-button click handler: if static facade → `activateFacade(facade, clampedStart)`; if active iframe → postMessage `seekTo` (~45 min)
- **C5.5** — a11y + keyboard nav verification + Lighthouse CLS check (~30 min)

## No-Gos

- No YouTube API library (we use postMessage directly; no gapi.js)
- No chapter editing UI (data is YouTube's, read-only)
- No chapter-list pagination (if a facade has > 6 chapters in its window — unlikely, max observed is 3 — collapse extras into a "+N more" disclosure)
- **No autoplay on page load or chapter render.** Autoplay is allowed ONLY after an explicit user click (facade OR chapter button). (Codex R2 P1 fix — wording ambiguity resolved.)
- No changes to facade thumbnail logic
- No cross-facade chapter linking (chapter in facade A can't jump to facade B's video)
- No seeking to chapter start BEFORE the facade window — always clamp to `facadeStart` for chapters starting pre-window (avoids leaking pre-facade content)
- No `start_time`/`end_time` variables in the built code — always normalize first (explicit build step)

## Verify

```bash
# Before
ls jarda-ai-start/docs/research/2026-04-21-round-2-research/*.json  # 4 JSON files
# After build
rg -n "videoChapters" jarda-ai-start/index.html  # expect 1+ match
rg -n "class=\"video-chapters\"" jarda-ai-start/index.html  # expect 7 matches (one per facade)
rg -n "postMessage.*seekTo\|func.*seekTo" jarda-ai-start/index.html  # expect 1+ match
rg -n "enablejsapi=1" jarda-ai-start/index.html  # expect presence in iframe src template
```

---

# C6 · Appendix voice tightening + redirects

**Appetite:** S · **Risk:** 2 · **Codex R2:** optional (skip recommended)

## Problem

Round 1 wanted to ADD 2 new appendix blocks ("pragmatic handoff note" + "evaluative"). Gemini v2 signal: appendix already feels like homework; adding more will backfire. User decision: REDIRECT — drop new blocks, cure 11GB in Stop 4 (handled by C3.c), codify the "write it down to stop forgetting" principle in Stop 6 as one line, leave existing 3 appendix blocks alone with minor voice-polish.

## Verified Assumptions

| Claim | Source | Verify |
|---|---|---|
| Appendix currently has exactly 3 blocks: Tool landscape, Market map, Why these six stops? | `index.html:1804, 1812, 1836` | rg -n "research-subtitle" jarda-ai-start/index.html → 3 matches |
| Stop 6 opens at `<section id="stop-6">` | `index.html` at `cf3e0a6` | rg -n 'id="stop-6"' jarda-ai-start/index.html |
| Stop 6 contains closing paragraph about codifying workflows | `index.html:1725-1770` | rg -n "stop-6-title\|first week\|operating" jarda-ai-start/index.html |
| Market map block content changes are handled by C1 (not C6) | this doc, C1 section | (no grep needed) |

## Shape

Two edits, both scoped to existing content:

### 6.a — Stop 6 principle codification line

Add one line to Stop 6's main rationale (or at the end of its summary block): something like *"What separates a workflow that sticks from one that evaporates is whether the decisions are written down. The agent can't remember what you never captured."* One sentence. Honest register.

### 6.b — Optional appendix voice polish

Light pass on existing 3 appendix blocks. Targets per Codex R1 P1 on C6 v1 ("voice drift on evaluative"):
- Market map intro currently has "A short list of other voices teaching in this space. Notes describe the shape of their output, not a verdict on it." — fine, keep.
- "Why these six stops?" has an evaluative-sounding "A few stops were considered and dropped." — acceptable.
- Light audit: any sentence in appendix that sounds like a product reviewer should go. Budget: 2-3 sentences max.

## Acceptance Criteria (block-local)

- [ ] Appendix block count unchanged (exactly 3: Tool landscape, Market map, Why these six stops?)
- [ ] Stop 6 has a new principle-codification line (grep for new phrase)
- [ ] No new blocks added anywhere
- [ ] Voice audit on appendix: no sentence sounds like a product review
- [ ] Market map block content is handled by C1, not C6 (C6 doesn't touch that block's voice)

## Slices

- **C6.1** — Stop 6 principle line insertion (~15 min)
- **C6.2** — Optional appendix voice polish (~20 min)

## No-Gos

- No new appendix blocks (violates Gemini overwhelm signal)
- No scope overlap with C1 (don't touch Market map block content)
- No scope overlap with C3 (don't address 11GB in C6)
- No added evaluative language
- No length increase per appendix block (net word count within ±10%)

## Verify

```bash
# C6 alone doesn't change block count (C7 handles expansion)
# Stop 6 principle line exists
rg -n "never captured\|write.*down\|stops evaporating" jarda-ai-start/index.html  # expect 1 match from C6
# Voice polish — no new evaluative language
rg -c "must-read\|game-changing\|the best\|definitive" jarda-ai-start/index.html  # expect 0
```

**Note:** C6's original "keep 3 appendix blocks" is superseded by C7, which expands the appendix with business-specific blocks. C6 now scopes to voice polish on the 3 existing blocks + Stop 6 principle line, without touching block count.

---

# C7 · Business-aware appendix + customization acknowledgment

**Appetite:** M-L · **Risk:** 4 · **Codex R2:** MANDATORY (competitor-naming + inference framing surface)

## Problem

The primer is built for one specific reader with an online-published business context: adventure-elopement photography in Sweden/CZ, a CZ-language book on 45 European peaks, a CZ podcast, architectural B2B photography, a guiding practice. Extensive research exists in `/Users/profile_1/Coding/jarda/discovery-plan.md` covering:

- Competitive landscape (Sweden/CZ wedding peers, adventure writing peers, aspirational brand models) — lines 52-77
- Growth gaps + opportunities (12 specific gaps: funnel integration, language repurposing, record visibility, anniversary engine, Rexby guide product, photo distribution across 14 marketplaces, 4 English-speaking audience segments) — lines 77-120
- SEO deep-research backing (AEO vs classic SEO, thebestviewpoints.com scan, agentic SEO stack recommendations, 8 concrete SEO recipes with paste-ready prompts, what NOT to automate) — lines 290-345

None of this business-specific value is in the primer today. Shipping only generic Cowork explanation misses the primer's biggest value-add: *how Cowork fits the reader's actual work*. Per user decision 2026-04-21: publish the reports in the appendix + acknowledge customization up front.

**Privacy model (confirmed by user):** keep `Jay Z` placeholder as reader's name; describe reader's niches WITHOUT linking his own URLs; name real competitors WITH URLs (public businesses); add `<meta name="robots" content="noindex,nofollow">` to `<head>` as safety net.

**Content principle:** nothing in this appendix leverages anything that isn't already public about either the reader or their competitors. Professional voice on competitors — no trash talk, no "laundering". Framing is "where Cowork creates leverage for this reader's niche", not "here's how to beat your competitors".

## Verified Assumptions

| Claim | Source of truth | Verify |
|---|---|---|
| discovery-plan.md has Competitive landscape section (line 52-77) with real competitor URLs | `/Users/profile_1/Coding/jarda/discovery-plan.md` | sed -n '52,77p' /Users/profile_1/Coding/jarda/discovery-plan.md |
| discovery-plan.md has Growth gaps section (line 77-120) with 12 gaps | `/Users/profile_1/Coding/jarda/discovery-plan.md` | sed -n '77,120p' /Users/profile_1/Coding/jarda/discovery-plan.md |
| discovery-plan.md has SEO section (line 290-345) with 8 concrete recipes | `/Users/profile_1/Coding/jarda/discovery-plan.md` | sed -n '290,345p' /Users/profile_1/Coding/jarda/discovery-plan.md |
| **`<meta name="robots" content="noindex, nofollow">` ALREADY exists** at line 8 of `<head>` (Codex R2 P1 fix; was wrongly claimed as missing) | `index.html:8` | rg -n 'name="robots"' jarda-ai-start/index.html → 1 match at line 8 |
| GDPR Art. 17 grants data subjects right to request erasure | [EUR-Lex GDPR consolidated text](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A02016R0679-20160504) Art. 17 | (external — re-verify at build if copy cites specific language) |
| France adopted a 2020 law specifically for child-influencer content: **Loi n° 2020-1266 du 19 octobre 2020 visant à encadrer l'exploitation commerciale de l'image d'enfants de seize ans sur les plateformes en ligne** | [Legifrance law text](https://www.legifrance.gouv.fr/jorf/id/JORFTEXT000042439054) · [Library of Congress summary](https://www.loc.gov/item/global-legal-monitor/2020-10-30/france-parliament-adopts-law-to-protect-child-influencers-on-social-media/) | (external — confirm name + date at build) |
| California SB 1247 (child-influencer bill) introduced Feb 19, 2026 — **bill status at shape time: introduced, not enacted** | [Leginfo CA SB 1247](https://leginfo.legislature.ca.gov/faces/billNavClient.xhtml?bill_id=202520260SB1247) | (external — re-check status at build; phrasing must say "introduced" not "passed") |
| Appendix is structured as `.research-block` divs at `index.html:1787-1843` | `index.html` at `cf3e0a6` | rg -n 'class="research-block"' jarda-ai-start/index.html → 3 matches |
| Current reader name throughout primer is `Jay Z` placeholder | `index.html` at `cf3e0a6` | rg -c "Jay Z\|Jay-Z" jarda-ai-start/index.html |
| Real name `Jarda` does not currently appear in index.html | `index.html` at `cf3e0a6` | rg -c "Jarda" jarda-ai-start/index.html → 0 |

## Shape

Four additions:

### 7.1 — Confirm existing `<meta name="robots">` tag

Already present at `index.html:8` with `content="noindex, nofollow"` (with space after comma). **Verify + no-op.** If build-pass finds the tag missing for any reason, add it back. Ensure exactly ONE robots meta tag (no duplicates). Accept both `noindex,nofollow` and `noindex, nofollow` comma spacings — either is valid.

### 7.2 — Customization-acknowledgment line (coordinates with C3.1 prereq card)

One sentence added to the C3 prereq/identity card:

> *"This primer is built for one reader — an adventure photographer and author with a specific set of online projects. The appendix maps how Cowork fits those niches specifically."*

The phrasing stays generic-enough to work without naming the reader's businesses but explicit enough that the customization doesn't feel accidental.

### 7.3 — Expand appendix: add Block D + Block E + Block F (3 new blocks + rename Block 2)

Final appendix block structure — **7 `.research-block` elements** (F+ is NOT a block; it's a bridge paragraph inside Block E's closing or between E/F — spec'd below):

| # | `.research-block` ID | Title | Source | Status |
|---|---|---|---|---|
| 1 | `id="research-tool-landscape"` | Tool landscape | existing | unchanged |
| 2 | `id="research-teaching-voices"` | Teaching voices | renamed via C1 | content swap |
| 3 | `id="research-market-playbooks"` | Your market: clusters, public patterns, Cowork playbooks | discovery-plan.md 52-77 | NEW (C7 Block D) |
| 4 | `id="research-growth-opportunities"` | Growth opportunities your Cowork habit can unlock | discovery-plan.md 77-120, prioritized | NEW (C7 Block E) |
| 5 | `id="research-seo-recipes"` | SEO in 2026 and 8 concrete Cowork prompts for your site | discovery-plan.md 290-345 | NEW (C7 Block F) |
| 6 | `id="research-ten-year-picture"` | The 10-year picture | Block G | NEW (C7 Block G) |
| 7 | `id="research-six-stops"` | Why these six stops? | existing | unchanged |

**Block F+ is a one-paragraph bridge, NOT a `.research-block`.** It sits as the closing paragraph of Block E (inside `id="research-growth-opportunities"`) or as a standalone `<p class="research-bridge">` between Blocks E and F — implementation choice during build. It must NOT carry a `.research-block` class (that would push the appendix to 8 blocks and break the count check).

**Stable ID requirement (convergent Codex R2 P1 fix):** every `.research-block` element MUST have one of the IDs above. This enables `sed -n '/id="..."/,/id="..."/p' | rg ...` for block-local Verify commands across C1/C7. Any Verify command that uses whole-file `rg` against appendix content is a P1 defect — scope it.

Gemini's overwhelm signal is mitigated because Block G is compact + Block F+ is one paragraph. Reader can skim (7 headings) or go deep (full content). Research-bundle links let depth live off-primer.

#### Block D — Your market: clusters, public patterns, Cowork playbooks

**Voice guardrail (applies to the entire block):** every observation about a competitor is an INFERENCE from their public output. Never claim a specific tool, vendor, or workflow a competitor uses unless a public source explicitly documents it. The honest register is *"From the outside, this looks like [pattern]. If you wanted to produce similar output, a Cowork setup would look like [playbook]."* Never *"They use Buffer + Zapier + ..."*.

**Framing paragraph (ship as opening sentences):**

> *"Your work sits across three markets and a fourth shape worth studying. Below: four clusters of peers, what's visible in their public output, and where a Cowork habit could scope out similar work for you. Two clusters get a closer look — the adventure-elopement peers (your closest market) and Honest Guide (a brand shape, not a competitor, worth adapting). The other two stay ideation-level: enough to point a direction, not enough to act on before you've done your own digging."*

**Then 4 clusters — 2 ZOOM, 2 IDEATION:**

---

**Cluster 1 — Adventure-elopement peers (CLOSE ZOOM)**

Peers: [Ceranna Photography](https://ceranna.com/) (Italy + CZ, adventure-elopement focused — closest peer), [Avvagraphy](https://www.avvagraphy.com/) (Prague duo, more traditional package model).

*Ceranna — what's visible:*
- Dual-market portfolio (Italy + CZ) with consistent voice across both languages — implies deliberate content adaptation, not just translation
- Adventure-elopement framing carries across the whole site (not a secondary offering) — means the inquiry flow is shaped for that audience
- Portfolio taxonomy by story rather than by venue or season — different indexing than a typical wedding-photo site

*If they're automating any of it, from the outside it would look like:*
- A shared voice-and-style doc that guides translation between CZ and Italian copy
- A repeatable inquiry-response shape that asks the right 4-5 questions upfront
- A post-shoot client log that feeds the next year's editorial calendar

*Your Cowork playbook for the same pattern:*
1. A **voice-and-style project** with a CZ/EN dual-voice guide in the Instructions file. Drop a CZ blog post → get an EN draft that sounds like you, not a translator.
2. An **inquiry-qualifier** workflow (Cowork skill): inbound email in, draft reply out, with the right qualifying questions baked in (date flexibility, location type, travel appetite, budget band).
3. A **shoot-log repurposer**: voice-note after each shoot, Cowork files it into the project, drafts a social caption + blog lede + newsletter paragraph from the same note.

*Avvagraphy — one-line read:* more traditional Prague-wedding positioning, less adventure-elopement. Useful as a reference for the "classical Prague duo" shape if the reader wants to keep one foot in that market.

---

**Cluster 2 — Swedish editorial wedding (IDEATION ONLY)**

Peers: [2 Brides (Isabelle Hesselberg)](https://2brides.se/), [Tanja Ferm](https://en.tanjametelitsa.com/brollopsfotograf-stockholm), [Evelyn Wallin](https://evelynwallin.com/cityhall-elopements/), [Daniel Notcake](https://en.danielnotcake.com/photographer_stockholm_sweden), Alessandro Castelli, John Hellström, Karin Lundin.

*Shared patterns visible from the outside:*
- Premium, editorial-dominant portfolios — the photography does the selling
- Most pick one lane (e.g., city hall elopements, editorial weddings) and double down
- Instagram is the primary inbound funnel; blogs are lighter / image-heavy
- Stockholm-area concentration; limited Scandinavia-wide positioning

*Where Cowork could help you in this cluster:* Instagram caption drafting that ties back to blog content and maintains consistent voice across 20+ posts a month; content adaptation to pull Scandinavia-wide positioning out of single-venue shoots.

**Ideation only — research each peer's public feed yourself before building workflows targeting their audience.** The observations above are directional; specific tactics need more looking.

---

**Cluster 3 — Adventure / travel writing (IDEATION ONLY)**

Peers: [Ben Love (Wild Guide to Scandinavia)](https://wildthingspublishing.com/product/wild-guide-to-scandinavia-book-norway-iceland-sweden-denmark/) — book publisher route, academic polish, 700 ideas. Christjan Ladurner — guide + heli-pilot + author, multi-hyphenate model. [Ladislav Zibura](https://www.zibura.cz/) — best-selling CZ travel author, walking pilgrimages, lyrical prose, strong domestic attention.

*Shared pattern from the outside:* each of these authors turns one trip or one region into multiple downstream assets — book chapter, essay, talk, podcast interview, guided trip. The asset-multiplication factor looks high.

*Where Cowork could scope it:* CZ podcast transcript → EN blog draft outline, EN blog post → CZ podcast show-notes, one trip report → book chapter structure. The [Podcast transcript → blog draft] recipe in Block F below is a concrete first step.

**Ideation only — the specific shape depends on which downstream channel you want to multiply into first. Pick one and try it; the others become obvious.**

---

**Cluster 4 — Aspirational brand shape (CLOSE ZOOM, non-competitive)**

Not a competitor — an adjacent brand worth studying: [Honest Guide (Prague)](https://www.youtube.com/c/HONESTGUIDE) by Janek Rubeš + Honza Mikulka.

*What's visible in their production:*
- Two-host YouTube channel, weekly-ish cadence, Czech-origin + English-speaking
- Authenticity contract: "local expert protects visitors from tourist traps, no BS, warm humor, earned POV"
- Each episode has a clear POV and a specific tourist trap to debunk — pattern repeats without feeling formulaic
- Cross-media reuse: YouTube → shorts → guidebook → live events

*If they're automating any piece of it, from the outside it could look like:*
- A shared episode structure doc ("hook, trap, debunk, alternative, wrap") that makes scripting fast
- A research pipeline that gathers local press + user-reported traps into a weekly digest
- Caption / thumbnail templates that keep visual consistency

*What's transferable for you (shape, not domain):*
- The authenticity-contract framing is the most valuable takeaway. Your adjacent angle: *"An honest guide through the Czech / European / Scandinavian mountains."* Same authenticity contract (first-person, earned credibility, record + 45 peaks + Stockholm base + bilingual audience as the credential), different domain.
- Their episode-structure pattern maps to your content: hook (dramatic summit photo), context (what most people miss), takeaway (what you'd actually do), alternative or next-step, wrap.

*Your Cowork playbook for the shape:*
1. **A brand-voice project** with the authenticity-contract phrasing pinned in Instructions. Every post gets voice-checked against it.
2. **An episode-structure skill**: given a trip report or summit photo, draft a post that uses the hook-context-takeaway-alternative-wrap shape in your voice.
3. **A research-digest skill** (adapted from Block F recipe 7): weekly summary of what's trending in Czech-speaking and English-speaking adventure communities, so your content references current conversations without you scrolling feeds.

---

**Your edge across all four clusters:**

*"Nobody in any of these clusters has your specific stack — adventure-mountain scenic photography + genuine mountaineering expertise + Guinness record + 45 European peaks book + Scandinavia base + bilingual audience. Most peers pick one lane. The leverage Cowork creates for you is not 'catch up to them' — it's 'make your hybrid reachable to more of the right people without the overhead growing with audience size.'"*

Voice check: every line above must read as honest inference, not verdict. If any observation sounds like "competitor X is doing it wrong", rewrite.

#### Block E — Growth opportunities your Cowork habit can unlock

Intro: *"A handful of specific openings where a Cowork habit moves the needle on your work. Each is grounded in what's already public about your online setup; each is something Cowork can make smaller with the right prompt habit."*

Pick 5-6 from discovery-plan.md's 12 gaps (the Cowork-relevant ones):

1. **Funnel integration** — blog (EN), portfolio (EN), book (CZ), podcast (CZ), Instagram don't cross-sell. No shared email list. Cowork fit: draft unified newsletter templates per audience segment.
2. **Language repurposing (91 CZ podcast episodes → EN goldmine)** — Claude drafts EN blog outlines from transcripts; you write the prose.
3. **Anniversary engine** — past wedding clients get no nurture. Auto-drafted reminders (you review + send) = referral pipeline.
4. **Book-to-leads bridge** — Czech book readers are ideal adventure-guide leads. Claude drafts opt-in landing copy in your voice.
5. **SEO systematization** — your blog already competes. Claude draft cadence 5x without losing voice. (See Block F for recipes.)
6. **Instagram ↔ long-form bridge** — Claude drafts caption-to-carousel and episode-to-carousel recipes.

Each bullet: 2-3 sentences max. No verdicts on whether the gap is "big" or "small" — just the pattern + the Cowork fit.

#### Block F+ — Force-multiplier note (between E and F)

One-paragraph bridge:

> *"One vertical compounds several of the items above: gear content. A gear list in your voice for each peak turns every blog post into affiliate revenue + lead-magnet fodder + a conditions-report asset. The full playbook — peer patterns, 3-tier Claude automation, European affiliate catalog — is in the research bundle at `docs/research/2026-04-21-round-2-research/gear-lists-business-research.md`. If you want the short version: start with one gear list for one peak, pick two affiliate programs (Bergfreunde.eu + Amazon DE), ship in three weeks, learn what converts, then scale with Claude."*

Points to `gear-lists-business-research.md` (3150 words, 24 sources) without inlining its depth. Keeps the primer lean; readers who want depth follow the link.

#### Block F — SEO in 2026 and 8 concrete Cowork prompts for your site

Intro: *"SEO shifted in 2026. Citations from ChatGPT, Perplexity, Google AI Overviews matter more than blue-link clicks. First 100-150 words of any post now double as the answer snippet. Below are 8 paste-ready Cowork prompts built for your site's niches. None of them write final posts — they draft outlines, do research, generate schema. You still write the prose."*

Then the 8 recipes from discovery-plan.md 318-337:

1. AEO intro rewriter
2. Peak-series outline generator
3. Seasonal publishing calendar
4. Image alt-text & caption batch
5. Schema markup generator (HowTo + Article + Person as JSON-LD)
6. Internal linking audit
7. AI-search citation check
8. Podcast transcript → blog draft

Each recipe gets: short description + the paste-ready prompt in a `<pre>` block.

Close the block with the discovery-plan's "What NOT to automate" list (3 items): no unsupervised full-post writing, no automated publishing, no keyword-chasing.

#### Block G — The 10-year picture (compact, ~400 words)

Final block before "Why these six stops?". Compact by design — more a closing orientation than another deep appendix.

**Draft content (ship as-is, refine in build):**

> **The 10-year picture**
>
> This primer ends where a 10-year arc begins. The creator whose work most closely rhymes with where you could go is [Paul Zizka](https://www.zizka.ca/) — a mountain photographer who moved to Banff with his wife, became a certified guide, built a business from one specific place over 15 years. Today: 8 books via Rocky Mountain Books, a 23,000-member online community called *Fuelled by Creativity*, clients including Apple and Arc'teryx. Not a celebrity — a specialist who compounded.
>
> **Three patterns show up in every trusted adventure-creator career** — whether [Chris Burkard](https://www.chrisburkard.com/), [Alex Strohl](https://www.alexstrohl.com/), [SectionHiker's Philip Werner](https://sectionhiker.com/philip-werner-bio/), or the paid-membership [Backpacking Light](https://backpackinglight.com) model:
>
> 1. *One specific place or niche, ten-year horizon.* Specificity beats breadth. Your particular mix — a published mountain project, regional guiding practice, bilingual audience — is already the thing. No need to broaden.
> 2. *Multi-stream revenue from day one.* Affiliate + books + prints + workshops + membership. No single stream is existential. The deep catalog is in the research bundle (`trust-family-business-models.md`).
> 3. *Say no to anything you wouldn't recommend for free.* Trust compounds slowly. The first cheap partnership is what kills credibility at year 7.
>
> **The family integration combo.** Every successful adventure creator who added a family — Zizka, Hilaree O'Neill, Alison Majka — converged on the same pattern: *home-base + regional adventures + partner-as-collaborator + kid-as-protagonist + content-archive-buffer + 4-stack revenue.* Big expeditions are optional when kids are small; regional access to your home range is the competitive edge.
>
> **Privacy-first, if it resonates.** When family appears in adventure content, you have a choice about how. The happy accident: the composition that defines premium adventure photography — silhouette, shot-from-behind, small figure in vast landscape — is also the safest composition for a kid. No trade-off between authentic family content and long-term respect for the child's future agency. If this direction sits right with you, a ten-rule playbook (pseudonym, delay-publish, strip EXIF, consent protocol by age, deletion ledger) and a Claude guardrail skill sit in the research bundle at `kid-privacy-best-practices.md`.
>
> **Worth considering now rather than later.** GDPR Art. 17 grants a child the right to request erasure when they come of age. France adopted a 2020 child-influencer law (Loi n° 2020-1266); California introduced SB 1247 in February 2026. The direction is clear enough even if no single jurisdiction has settled. Creators who build privacy-first early get to keep compounding; the others will have cleanup. Not urgent today — worth the hour of setup when the need arrives.
>
> **What to test every decision against:** *does this move toward Zizka's 10-year stack, or away from it?* If it doesn't, say no, even if it's flattering in the short term.

**Privacy-fingerprint gate (Codex R2 P0.1 fix):** Block G must NOT ship the deanonymizing combination "Guinness record + 45 European peaks + Stockholm base + bilingual audience". That fingerprint was in the earlier draft and was caught by Codex R2 as a denylist bypass — the placeholder persona fails when the text itself describes the reader's unique stack. Current draft (above) replaces with generic descriptors: *"published mountain project, regional guiding practice, bilingual audience"*. Verify during build: `rg -i "guinness\|45 peak\|45 european" index.html` → expect 0 matches.

Keep to ~400 words. Reference — don't inline — the research-bundle depth. The primer is the cartography; the research bundle is the terrain.

## Acceptance Criteria (block-local)

- [ ] `<meta name="robots" content="noindex,nofollow">` present in `<head>`
- [ ] Customization-acknowledgment sentence present in C3 prereq card (shared between C3 + C7 — either cluster can land it, but only one copy in final doc)
- [ ] Block D structured as 4 clusters (2 ZOOM: adventure-elopement peers + Honest Guide; 2 IDEATION: Swedish editorial + adventure writing)
- [ ] Each ZOOM cluster includes: (a) public observations, (b) "if they were automating this, it'd look like" inferences clearly marked as speculation, (c) Cowork playbook with 2-3 concrete workflow ideas
- [ ] Each IDEATION cluster includes: (a) shared pattern observation in 2-4 sentences, (b) 1-2 Cowork angle ideas, (c) explicit "ideation only — research more before acting" framing
- [ ] Block D names ≥6 real competitors WITH URLs (minimum: Ceranna Photography, Avvagraphy, 2 Brides, Tanja Ferm, Ben Love, Zibura, Honest Guide)
- [ ] Block D voice: never "X is doing it wrong / weak / failing / outdated"; inference register, not verdict
- [ ] Every automation-pattern claim about a competitor includes hedging language ("from the outside", "if they're automating", "appears to", "seems to") — verbatim as-speculation cues
- [ ] Block E lists 5-6 growth opportunities, each tied to a Cowork pattern
- [ ] Block F contains 8 SEO recipes with paste-ready prompts in `<pre>` blocks + "What NOT to automate" list
- [ ] Appendix has exactly 7 `.research-block` elements (Tool landscape + Teaching voices + D + E + F + G + Why six stops?). Verify: `rg -c 'class="research-block"' index.html` → **7**.
- [ ] Each of the 7 blocks has its stable `id` per table in §"Final appendix block structure". Verify: `for id in research-tool-landscape research-teaching-voices research-market-playbooks research-growth-opportunities research-seo-recipes research-ten-year-picture research-six-stops; do rg -c "id=\"$id\"" index.html; done` → each returns 1.
- [ ] Block F+ bridge exists but is NOT a `.research-block` (no `class="research-block"` on the F+ element). Verify: inspect the element between Block E content and Block F opening heading.
- [ ] Block G content: ~400 words, references Zizka + 3 trust patterns + family combo + privacy-first moat, links to `trust-family-business-models.md` and `kid-privacy-best-practices.md`. Verify: `sed -n '/id="research-ten-year-picture"/,/id="research-six-stops"/p' index.html | wc -w` → 300-500.
- [ ] Block G does NOT inline the 10 kid-privacy rules, the 10-channel revenue catalog, or the full trust archetype analysis.
- [ ] **Privacy-fingerprint check:** `rg -i "guinness\|45 peak\|45 european\|stockholm" index.html` → 0 matches in Block G (may match elsewhere if elsewhere is generic). Restrict check: `sed -n '/id="research-ten-year-picture"/,/id="research-six-stops"/p' index.html | rg -ci "guinness\|45 peak\|45 european"` → 0.
- [ ] **Legal claims in Block G** cite specific sources/dates: GDPR Art. 17 + Loi n° 2020-1266 + California SB 1247 (introduced Feb 2026, status: introduced not passed). Verify: `sed -n '/id="research-ten-year-picture"/,/id="research-six-stops"/p' index.html | rg "2020-1266\|SB 1247\|Art\\. 17"` → expect ≥2 citations in context.
- [ ] `<meta name="robots" content="noindex, nofollow">` present in `<head>` (existing, confirmed no duplicates added). Verify: `rg -c 'name="robots"' index.html` → exactly 1.
- [ ] No real-name "Jarda" / "Jarda Zaoral" anywhere (grep returns 0)
- [ ] No reader's own URLs: `thebestviewpoints.com`, `korunaevropy`, `jardaphoto`, `instagram.com/jarda*` (grep returns 0)
- [ ] Reader's business context described without naming him
- [ ] Lighthouse a11y ≥ 0.95 (appendix content is readable + structured)
- [ ] Block D total word budget between 1800-2500 words (enough for 2 zooms; not bloated)

## Slices

- **C7.1** — noindex meta tag (2 min, ship immediately — can run before Codex R2)
- **C7.2** — acknowledgment sentence in C3 prereq card (5 min if C3 landed first, else coordinate)
- **C7.3a** — Block D cluster 1 ZOOM: Adventure-elopement peers (Ceranna + Avvagraphy) with observations + Cowork playbook (~60 min)
- **C7.3b** — Block D cluster 2 + 3 IDEATION: Swedish editorial + adventure writing, surface-level only with "research more before acting" framing (~45 min)
- **C7.3c** — Block D cluster 4 ZOOM: Honest Guide shape + authenticity-contract framing + Cowork playbook (~45 min)
- **C7.3d** — Block D closing: "your edge across clusters" paragraph (~15 min)
- **C7.4** — Block E: Growth opportunities (~60 min)
- **C7.5** — Block F: SEO + 8 recipes (~90 min; paste-ready prompts require care — each is ~100 words)
- **C7.5b** — Block F+ one-paragraph bridge pointing at gear-content research (~10 min)
- **C7.5c** — Block G: The 10-year picture (~45 min; compact ~400 words, Zizka reference, 3 trust patterns, family combo, privacy-first moat, 2 research-bundle links)
- **C7.6** — voice audit pass on all new blocks including F+ and G; verify hedging language present in every competitor-automation claim; final name/URL denylist grep (45 min)

## No-Gos

- No reader's real name in the public page (keep `Jay Z` placeholder)
- No reader's own business URLs linked (descriptions only; if a URL would make a recipe more concrete, describe instead of link)
- No unflattering competitor characterizations — professional voice throughout
- No content not already publicly available about either reader or competitors
- **No specific tool/vendor claims about a competitor without evidence.** NEVER: "Ceranna uses Buffer", "2 Brides runs Zapier", "Honest Guide edits in Premiere". ALWAYS: "From the outside, this pattern looks like [shape]." "If they're automating this, it could look like [pattern]." Verdict-free inference only.
- No "reverse-engineering" language that implies industrial-espionage intent. Frame as "what's visible in their public output + how you'd scope similar work if you wanted".
- No ZOOM on more than 2 clusters (keeps Block D word budget bounded; avoids overwhelm Gemini flagged)
- No IDEATION cluster longer than 4 sentences of pattern observation (these are pointers, not deep dives)
- No recommendations that require revealing anything private
- No new SEO recipes beyond the 8 from discovery-plan.md (keep scope bounded)
- No claim about competitor pricing, client counts, or revenue
- No affiliate links or referral tracking
- No deep dive into every opportunity ourselves — the reader does their own digging before acting on ideation-cluster observations
- **Block G must stay ≤ 500 words.** The 10-year picture is a compact closing orientation, not another deep appendix. Depth lives in the research bundle.
- **Block G does NOT inline the 10 kid-privacy rules, the 10-channel revenue catalog, the 4 trust archetypes, or the detailed family-integration case studies.** Those are operational research artifacts for the reader — they sit in `docs/research/2026-04-21-round-2-research/` and get linked from Block G, not reproduced.
- Block G must not contain identifying details about the reader (no "Koruna Evropy", no specific peak names tied to him, no personal URLs) — keep Jay Z placeholder voice.

## Verify

```bash
# noindex present
rg -n 'name="robots"' jarda-ai-start/index.html  # expect 1 with noindex
# Real name never ships
rg -ci "jarda" jarda-ai-start/index.html  # expect 0
# Reader's own URLs never ship
rg -ci "thebestviewpoints|korunaevropy|jardaphoto" jarda-ai-start/index.html  # expect 0
# Competitor URLs DO ship
rg -c "2brides.se|ceranna.com|zibura.cz|wildthingspublishing.com|danielnotcake.com" jarda-ai-start/index.html  # expect ≥5
# Block count
rg -c 'class="research-block"' jarda-ai-start/index.html  # expect 7
# Block G exists + is compact
rg -n "10-year picture\|Zizka\|privacy-first" jarda-ai-start/index.html  # expect ≥3 matches in Block G
python3 -c "import re; c=open('jarda-ai-start/index.html').read(); m=re.search(r'10-year picture(.*?)Why these six stops', c, re.DOTALL); print('Block G words:', len(m.group(1).split()) if m else 'N/A')"
# Expect Block G: 300-500 words; fail if >500
# Block G references research bundle
rg -c "trust-family-business-models.md\|kid-privacy-best-practices.md\|gear-lists-business-research.md" jarda-ai-start/index.html  # expect ≥3 (F+ gear + G trust + G privacy)
# Voice — no trash talk
rg -ci "inferior|weak|failing|losing|outdated|behind" jarda-ai-start/index.html  # expect 0 matches in new blocks
# Hedging language present for every competitor-automation claim
rg -c "from the outside|if they're automating|appears to|seems to|visible in" jarda-ai-start/index.html  # expect ≥5 matches in Block D
# No claims of specific tools used by competitors (common offending tool names)
rg -ci "uses buffer|uses zapier|runs airtable|edits in premiere|their stack is" jarda-ai-start/index.html  # expect 0
# Ideation-cluster framing explicit
rg -c "ideation only|research.*before acting|research more" jarda-ai-start/index.html  # expect ≥2 (one per ideation cluster)
# SEO recipes present
rg -c "AEO intro rewriter|Schema markup generator|Peak-series outline" jarda-ai-start/index.html  # expect 3+
# Acknowledgment line
rg -n "built for one reader" jarda-ai-start/index.html  # expect 1 match (in prereq card)
# Block D word budget sanity check (uses stable appendix IDs, not landmark text)
python3 -c "import re; c=open('jarda-ai-start/index.html').read(); m=re.search(r'id=\"research-market-playbooks\"(.*?)id=\"research-growth-opportunities\"', c, re.DOTALL); print('Block D words:', len(m.group(1).split()) if m else 'N/A')"
# Expect 1800-2500 words
```

---

## 3 · Codex R2 dispatch protocol

After user approves this master shape, dispatch 5 separate Codex reviews — one per MANDATORY or RECOMMENDED section (C2, C3, C4a, C5, C7). Not as one giant review of the whole doc (hurts review depth).

Each dispatch prompt template (fill `<CLUSTER>`):

```
You are reviewing cluster <CLUSTER> of the Round 2 Master Shape for Jarda AI-Start.
Read ONLY section <CLUSTER> at docs/plans/2026-04-21-round-2-master.md (skip other clusters).

This is ROUND 2 of a shape review cycle. Round 1 on the separate cluster
contracts (docs/plans/2026-04-21-cluster-*.md) produced:
- C2: APPROVE_WITH_REV (P1s: IO fallback, a11y/touch split, go/no-go thresholds)
- C3: REJECTED (scope too narrow; THIS v2 is intentionally expanded to address)
- C4: REJECTED (too many shape-changes; THIS v2 splits into C4a + C4b)
- C5: REJECTED (unverified chapter data; THIS v2 has persisted yt-dlp JSONs as VAs)

The full Round 1 reviews are at docs/research/2026-04-21-round-2-research/
codex-cluster-{1-6}-*.md.

Verdict format: APPROVE | APPROVE_WITH_REVISIONS | REJECT, with P0 blockers first,
P1 revisions second, P2 nits last. Focus on:
- Are Round 1 P0s addressed?
- Are new P0s introduced by the refactor?
- Is the AC block-local enough to pass preflight-aggregator?
- Are Verified Assumptions grep-verified, or memory-based?
- Any cross-cluster conflicts with C1/C4b/C6 (which you don't have) that appear
  from the cross-reference text in this section?
```

Dispatch them in parallel — `codex exec -p <prompt>` × 5. Save outputs to:
- `docs/research/2026-04-21-round-2-research/codex-R2-C2.md`
- `docs/research/2026-04-21-round-2-research/codex-R2-C3.md`
- `docs/research/2026-04-21-round-2-research/codex-R2-C4a.md`
- `docs/research/2026-04-21-round-2-research/codex-R2-C5.md`
- `docs/research/2026-04-21-round-2-research/codex-R2-C7.md` (business-appendix voice audit — focus on competitor framing + privacy denylist integrity)

Fold P0s back into this master doc. Commit.

---

## 4 · Privacy review (every build) — manual, not automated

**Audit script is DISABLED as a gate for this primer** (per user decision 2026-04-21). The script at `/Users/profile_1/Coding/jarda/scripts/privacy-audit.sh` stays in umbrella for future projects; it does NOT run automatically in this repo's build/push workflow.

Manual review checklist before every push (run by the committer, no script):

```bash
# Real name never in public file
rg -ci "jarda" jarda-ai-start/index.html   # expect 0
# Reader's own URLs never in public file
rg -ci "thebestviewpoints|korunaevropy|jardaphoto|instagram\.com/jarda" jarda-ai-start/index.html  # expect 0
# Referral codes, credentials (standard sensitive patterns)
rg -c "api_key|API_KEY|bearer|secret_key|referral_code|aff_id" jarda-ai-start/  # expect 0
# noindex meta present
rg -n 'name="robots".*noindex' jarda-ai-start/index.html  # expect 1 (after C7.1 ships)
```

If any grep returns a match → stop, investigate, fix before pushing.

---

## 5 · Out of scope (explicitly)

- No new stops
- No new framework, no build tooling
- No telemetry / analytics
- No account signup flow
- No take-down automation (30-day window handled manually)
- No internationalization
- No additional research streams (3 UX + Codex R1 is sufficient)
- No third Gemini round
- No Cowork integration (the primer is about Cowork; it doesn't USE it)

---

## 6 · Decision log

| # | Decision | Resolution | Locked in |
|---|---|---|---|
| 1 | C3 scope breadth | WIDE (all 6 items absorbed) | umbrella `15cb892` |
| 2 | C4 split | SPLIT into C4a (structural) + C4b (voice) | umbrella `15cb892` |
| 3 | C6 direction (original) | REDIRECT (no new blocks; 11GB→C3; principle→Stop 6) — superseded for block-count by C7 which intentionally expands the appendix | umbrella `15cb892` |
| 4 | C1 voice prefix | DROPPED entirely | umbrella `15cb892` |
| 5 | Round-2 execution shape | Path B+ Hybrid (one master doc, Codex R2 on 5) | umbrella `15cb892` |
| 6 | C1 three voices | Ruben Hassid + Jeff Su + Jesse Genet (drop Jack Roberts from appendix since he's in Stop 4 facade) | this doc (master shape) |
| 7 | Persona + naming in public repo | Keep `Jay Z` placeholder. Describe reader's business niches without linking his own URLs. Name competitors WITH URLs (public businesses). Add `<meta robots noindex,nofollow>`. | this doc (master shape) |
| 8 | Privacy audit script | DISABLED as a gate for this primer. Manual review replaces it. Script stays in umbrella for future use. | this doc (master shape) |
| 9 | C7 scope | Add new cluster for business-aware appendix (Blocks D/E/F) + customization acknowledgment + noindex meta. Recommended (not mandatory) Codex R2 given competitor-naming surface. | this doc (master shape) |
| 10 | C7 Block D structure | Cluster competitors into 4 groups (adventure-elopement peers, Swedish editorial, adventure writing, aspirational brand). ZOOM on 2 (adventure-elopement + Honest Guide — closest peer + most instructive brand shape). IDEATION on 2 (Swedish editorial + adventure writing — pointers only, reader digs deeper). Reverse-engineer OBSERVABLE patterns from public output; never claim specific tools without evidence; Cowork playbook per ZOOM cluster. Risk bumps from 3-4 to 4; Codex R2 escalates from recommended to MANDATORY. | this doc (master shape) |
| 11 | Opportunity scoring + Code escalation ladder | 12 opportunities scored by Gemini + Codex in parallel → consensus top 5 (#2, #1, #11, #3, #8) with dependency sequence + 3 items worth more research (#6, #9, #10). 3 Code-escalation candidates (#8, #11, #12) identified for beyond-Cowork batch mode. 2 on-brand SVG infographics hand-crafted (`opportunity-matrix.svg` 2×2 + `cowork-to-code-ladder.svg` 3-phase). Force-multiplier: gear content compounds #1/#3/#8/#11. All persisted to research bundle. | commit 9f354d3 |
| 12 | Gear-content vertical | Research brief (3150 words, 24 sources) covers affiliate economics (4-12% on $120-175 orders, EU programs = Bergfreunde + Alpinetrek + Amazon DE), 3 peer patterns (practitioner what's-in-my-bag, deep-editorial Skurka+OGL, paid PDF + Skurka-bundled model), 8 structural elements that convert, 3-tier Claude automation (Cowork project + connectors + Code batch). Framed as FORCE-MULTIPLIER across existing #1/#3/#7/#8/#10/#11 rather than standalone #13. Block F+ one-paragraph bridge references the brief without inlining. | commit ca99bc7 |
| 13 | Trust + family + business-model research | 4 archetypes of trusted creators (independent reviewer, industrial testing, membership-funded, career-arc photographer). Paul Zizka identified as closest template for reader (Banff + 8 books + 23K-member community). 6 trust-compounding patterns. 10-channel revenue catalog. Family-integration combo named (home-base + regional + partner-as-collaborator + kid-as-protagonist + content-archive + 4-stack revenue). loudavymkrokem.cz extractable patterns (5-stream revenue, multi-language, Patreon — NOT their make-money-online course genre). Feeds Block G. | commit fad67fe |
| 14 | Kid privacy research + operational policy | 10-rule guardrail for kid content (pseudonym, silhouette/back-only, delay-publish 3-6mo, strip EXIF, no school/home/medical/bath/distress, two-account split, age-banded consent, deletion ledger, partner's agency is her own, digital will). GDPR framework (Art. 6/8/12/17). France 2020 + California 2026 child-influencer laws. **Happy accident:** adventure-photography's silhouette-first composition IS the gold-standard privacy technique — zero trade-off. Claude automation: #6.2 kid-content guardrail skill + deletion ledger + Art. 17 response kit. Feeds Block G privacy-first moat paragraph. | commit (this one) |
| 15 | C7 Block G addition | NEW Block G "The 10-year picture" — compact ~400-word closing orientation for the primer. Contains: Zizka template + 3 trust patterns (one place/ten-year horizon, multi-stream, say-no) + family-integration combo + privacy-first moat. Links to `trust-family-business-models.md`, `kid-privacy-best-practices.md`, `gear-lists-business-research.md` for depth. Hard no-inline: keep Block G ≤ 500 words, let research bundle carry the depth. | this doc (master shape) |

---

*End of round-2 master shape doc. Next actions: (1) user reviews + approves; (2) dispatch Codex R2 ×4 in parallel; (3) fold P0s; (4) begin builds in dependency order per §2.*
