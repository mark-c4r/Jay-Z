---
ticket: jarda-ai-start/v2-restructure
status: completed
appetite: XL (split into v2a ~8–10h + v2b ~4–6h)
risk_score: 2
project: jarda-ai-start
updated: 2026-04-21
supersedes: 2026-04-20-onboarding-page-v1.md
files:
  - jarda-ai-start/index.html
  - jarda-ai-start/assets/hero-summit.jpg
  - jarda-ai-start/assets/diagrams/*.svg
  - jarda-ai-start/excalidraw-source/*.excalidraw
  - jarda-ai-start/assets/diagrams/_style-guide.md
  - jarda-ai-start/README.md
  - jarda/.gitignore
  - jarda/jarda-private/aerox-office-review.md
  - jarda/jarda-private/research-notes.md
  - scripts/privacy-audit.sh
---

# Jarda AI-Start — v2 Redesign

## Problem

v1 shipped clean (Lighthouse 100/100, privacy denylist passing) but reads as "a nice landing page," not "a sober primer from someone who figured Cowork out." Session 2's round 6 prompt (*"a bigger deeper rethink of the whole structure"*) called this out directly. Concrete failure state: Jarda opens v1 on his phone, sees five parallel tabs with "6 Wins" as chapter timestamps (no embedded video), hits starter prompts laced with `{your region}` / `{notable credential}` placeholder slots that read as stalking, sees no demonstration of WHY these recommendations are right — and closes the tab. The 4-reviewer cross-model round (Codex / Gemini / Chief Designer / Chief of Staff) confirmed: structure flat, content underused, rationale invisible, voice chirpy, visuals monotone. v2 reshapes the site as a 6-stop video-first course with visible spine + optional branches + public research appendix, driven by the principle **"in control, not under control."**

## Verified Assumptions

| Claim | Source | Status | Verified At | Verify |
|-------|--------|--------|-------------|--------|
| v1 index.html defines STORAGE_KEY `ai-start-onboarding-state` | `jarda-ai-start/index.html:2157` | VERIFIED | 2026-04-21T14:00:00-0500 | grep -c "ai-start-onboarding-state" jarda-ai-start/index.html |
| Triglav hero image exists at `jarda-ai-start/assets/hero-view.jpg` | `jarda-ai-start/assets/hero-view.jpg` | VERIFIED | 2026-04-21T14:00:00-0500 | test -f jarda-ai-start/assets/hero-view.jpg |
| 5 transcripts totaling ~67k words exist at `jarda/transcripts/` | `jarda/transcripts/` | VERIFIED | 2026-04-21T14:00:00-0500 | test $(ls jarda/transcripts/*.txt \| wc -l) -eq 5 |
| v1 plan exists at `jarda-ai-start/docs/plans/2026-04-20-onboarding-page-v1.md` | `jarda-ai-start/docs/plans/` | VERIFIED | 2026-04-21T14:00:00-0500 | test -f jarda-ai-start/docs/plans/2026-04-20-onboarding-page-v1.md |
| v1 uses tab-button SPA structure | `jarda-ai-start/index.html` | VERIFIED | 2026-04-21T14:00:00-0500 | grep -c "tab-button" jarda-ai-start/index.html |
| Public repo name is `Jay-Z` (privacy decision D2/D11) | `jarda/CONTEXT.md` | VERIFIED | 2026-04-21T14:00:00-0500 | grep -n "Jay-Z" jarda/CONTEXT.md |

## Shape Decision

Full rewrite of `jarda-ai-start/index.html` as a single-page 6-stop video-first course, split into two shipping phases for risk management: **v2a** (stops 1–3 + full navigation shell + 3 Excalidraw diagrams, ~8–10h) ships first and gets a 7-day verify window with Jarda before **v2b** (stops 4–6 + completion state + public appendix, ~4–6h) commences. Each stop is 2–4 blocks mixing video embed + paraphrased highlights side-by-side, Excalidraw diagram, optional short reading, and safety-wrapped try-one prompt. Navigation chrome (sticky top + expanded left rail with block-dot progress + sticky bottom nav on mobile; hamburger on drawer-side) keeps progress + control always visible. Voice register is descriptive/matter-of-fact (normal-dude, friend-from-highschool, not sycophantic). Personalization dial is LOW — no hero at top, Triglav repurposed as a completion summit after Stop 6's try-one, branches are pure shape-of-work labels (Personal · Creative · Client · Deeper) without domain taglines. Page is short-lived (planned takedown ≤30 days post-handoff), so no SEO, analytics, or evergreen investments.

## Measurement Design

**What does this subsystem do, and who consumes its output?**
The page is a one-to-one handoff artifact — produces a primer experience consumable by one specific reader (Jarda). No downstream systems. Lifecycle: Jarda reads → copies what he wants into his own notes → Mark takes the page down (≤30 days).

**How will we know this change made it better?**
Qualitative rubric, measured via Mark's conversation with Jarda over 2 weeks post-v2a ship:
- Jarda opens the link within 48 hours
- Jarda completes Stop 1 without a clarifying DM or call
- Jarda runs at least one try-one in his actual Cowork within 7 days
- Jarda can explain what Cowork is in his own words (confirmed via DM)
- Jarda reaches Stop 3 within 3 days — **verify gate**: if stalls at Stop 2, v2b waits until blocker understood
- Jarda uses one thing from the page in real work within 2 weeks

Baseline: v1 was sent, Jarda opened briefly, didn't follow through on his own.

**What could get worse?**
Guardrail: Jarda feels over-personalized/stalked ("Mark has a dossier on me") OR under-personalized (feels generic). Measure via direct DM feedback from Jarda within 7 days ("did this feel like it was made for you?"). Target: the reader experiences "made for me" *without* experiencing "profiled me."

## Acceptance Criteria — v2a

- [ ] Stops 1, 2, 3 fully populated; stops 4–6 show "Coming in a few days" placeholder cards in the spine
- [ ] Navigation shell complete at all viewport widths (desktop ≥1200: 230px rail; 900–1200: 180px rail; tablet 768–900: single-column with hamburger; mobile <768: drawer on left)
- [ ] 3 Excalidraw diagrams rendered (Stop 1 positioning, Stop 2 project anatomy, Stop 3 memory scopes) with style-guide consistency (2px strokes, #222/#a84b2b ink, Inter labels)
- [ ] Branch chips show clean labels only (Personal / Creative / Client / Deeper) — no domain taglines on chips themselves
- [ ] Branch drawers open with general-principle content + one neutral example (not "as a photographer")
- [ ] LocalStorage v4 fresh-state on load (v3 key detected → deleted; no migration logic)
- [ ] Voice grep clean (0 hits on chirpy markers outside block quotes)
- [ ] Privacy grep clean (denylist + URL-encoded + case-variant + hyphen-variant + referral URL regex)
- [ ] Lighthouse a11y ≥95
- [ ] YouTube timestamp chips work (iframe seekTo() OR native `?t=` fallback on Safari private / uMatrix)
- [ ] Deployed to `Jay-Z` GitHub Pages; URL sent to Jarda
- [ ] Private appendix at `jarda/jarda-private/` exists with 2 stub markdown files
- [ ] `jarda/.gitignore` includes `jarda-private/`

## Acceptance Criteria — v2b (activated after v2a-verify signal)

- [ ] Stops 4, 5, 6 fully populated with full block compositions
- [ ] 3 more Excalidraw diagrams (Stop 4 connector scope, Stop 5 workflow anatomy, Stop 6 habit loop)
- [ ] Completion state: Stop 6 try-one checkbox → Triglav reveal + caption + one of 3 completion-copy candidates; reversible (uncheck hides)
- [ ] Public appendix populated: tool landscape (~250 words), market map (~400 words, 6 named competitors), "why these 6 stops" (~150 words)
- [ ] Callbacks from Stop 1 rationale + completion moment link to `Research · how these picks landed` rail entry
- [ ] All pre-ship verification commands exit 0 (13 v2a items re-green + 6 v2b-specific items green = 19 total)

## Slices

### Slice 1 (v2a): Navigation shell + Stop 1 — downhill

**Demo:** Open page at desktop + tablet + mobile. Sticky top bar shows "Stop 1 of 6 · Memory" + thin progress bar + block counter. Left rail lists 6 stops (2–6 labeled "Coming"). Bottom stop-nav shows prev/jump/next. Mobile hamburger opens drawer from left. Stop 1 has video embed + 3–4 paraphrased highlights side-by-side, try-one block, 4 branch chips, Excalidraw positioning diagram.

**Files:**
- `jarda-ai-start/index.html` (skeleton + Stop 1)
- `jarda-ai-start/assets/diagrams/stop-1-positioning.svg` + `.excalidraw` source
- `jarda-ai-start/assets/diagrams/_style-guide.md`
- `jarda-ai-start/README.md`

**Steps:**
1. Preserve v1 `<style>` palette tokens (Inter + Fraunces italic + near-white/ink/accent). Delete v1 body content.
2. Build HTML skeleton: sticky top (stop counter + progress bar + block counter), left rail (6 stops listed), main content, sticky bottom nav, mobile drawer container.
3. Wire rail navigation (click any stop → scroll + focus; localStorage tracks completed stops). Z-index hierarchy: drawer (40, fixed) > backdrop (30, fixed) > sticky top (20) > sticky bottom (20) > content (0). Drawer-open hides bottom nav.
4. Implement mobile drawer: ☰ on LEFT (matches drawer origin), slide-in 85vw, dim backdrop, ESC + backdrop closes, focus trap, return focus to ☰ on close.
5. Implement top bar — NO time estimates, block counter per-stop.
6. Draft Stop 1 content: 2–3 sentence rationale (descriptive/matter-of-fact voice), embed Jeff Su intro 3-min clip, 3–4 paraphrased highlights with timestamps (native `?t=` fallback href), one try-one prompt (safety-wrapped, neutral example), 4 branch chips + drawer stubs.
7. Write Excalidraw style guide. Create Stop 1 Excalidraw diagram (Cowork vs Code vs ChatGPT vs Codex positioning). Export SVG.

**Tests:**
- Visual diff at 1200 / 900 / 768 / 375 against `~/Coding/jarda/.superpowers/brainstorm/50244-1776751572/content/stop-pattern.html` + `mobile.html` mockups
- Tab-key navigates in logical order (rail → content → bottom nav); ESC closes drawer; focus returns to ☰
- Click timestamp chip → iframe seekTo() succeeds OR href opens YouTube in new tab with `?t=`
- Simulate iframe seekTo() failure (Safari private / uMatrix blocks) → confirm fallback href opens YouTube with `?t=SECONDS` parameter in new tab (test via mocking `window.YT` to undefined)
- On load with existing v3 key: key deleted, fresh v4 state written

**Depends on:** nothing

### Slice 2 (v2a): Stops 2 + 3 + their diagrams — downhill

**Demo:** Click through Stops 1 → 2 → 3 via rail, bottom nav, and "jump to any." Each has full block composition. All 12 branch drawers (3 stops × 4 branches) open inline with general-principle content.

**Files:**
- `jarda-ai-start/index.html` (Stop 2 + 3 content + all 12 branch drawers)
- `jarda-ai-start/assets/diagrams/stop-2-project-anatomy.svg` + source
- `jarda-ai-start/assets/diagrams/stop-3-memory-scopes.svg` + source

**Steps:**
1. Extract Jeff Su transcript (`jarda/transcripts/jeff-su-cowork-80pct.txt`) — pull project section (Stop 2) and memory section (Stop 3) with timestamps; paraphrase 3–4 highlights each.
2. Draft Stop 2 + Stop 3 try-one prompts (safety-wrapped, neutral).
3. Write 12 branch drawers (Stops 1–3 × 4 branches): ~50–80 words each. Pattern: general principle + one neutral example. No "as a photographer" / "for your business."
4. Create Stop 2 Excalidraw (project anatomy: instructions + files + memory) per style guide.
5. Create Stop 3 Excalidraw (memory scopes: system / project / chat nested) per style guide.
6. Branch drawer mechanic: inline expand if content <3 viewport heights; else slide-over with focus trap.

**Tests:**
- Navigate Stop 1 → 2 → 3 via each nav mechanism; localStorage tracks per-stop and per-block completion
- Each branch chip on each stop opens correctly; drawer content is domain-neutral (no "kids", "photo", "business" language inside stated shape)
- 375px viewport: all stops render without horizontal scroll; stacked blocks rhythm holds

**Depends on:** Slice 1

### Slice 3 (v2a): Voice + privacy + a11y pass — downhill

**Demo:** All preflight checks green — voice grep clean, privacy grep clean, Lighthouse a11y ≥95, LCP <2.5s throttled 3G.

**Files:**
- `jarda-ai-start/index.html` (copyedit pass)
- `scripts/privacy-audit.sh` (new)

**Steps:**
1. Write `scripts/privacy-audit.sh` — denylist patterns (concrete examples, patterns maintained in the script itself): literal names (`Jarda`, `jarda`, `JARDA`, `Jarda Zaoral`, `Jarda-Zaoral`), URL-encoded variants (`Jarda%20Zaoral`, `Jarda%2DZaoral`), case-variants including Czech diacritics (`Jardá`, `Jardak`), hyphen-variants (`jarda-zaoral`, `jardazaoral`), referral URL regex (`utm_source=.*jarda.*|ref=.*jarda.*` case-insensitive). Script exits 1 on any hit; exits 0 on clean.
2. Voice grep pass: `grep -En '!|\bamazing\b|\bpowerful\b|\btruly\b|\bexciting\b|let'"'"'s dive in|\btogether\b|just for you' jarda-ai-start/index.html` — fix hits outside block quotes.
3. Run `bash scripts/privacy-audit.sh jarda-ai-start/index.html` — exit 0 required.
4. Run Lighthouse (mobile + desktop throttled) — a11y ≥95 required.
5. Keyboard-only manual pass: all stops + branches + skip/jump reachable.

**Tests:**
- `bash scripts/privacy-audit.sh` → exit 0
- Lighthouse a11y score JSON committed to `docs/verification/2026-04-21-v2a-lighthouse.json`
- `grep -cE 'Personal.*kids|Creative.*photo|Client.*business|your family' jarda-ai-start/index.html` → 0

**Depends on:** Slice 2

### Slice 4 (v2a): Deploy v2a + open verify gate — downhill

**Demo:** Live URL sent to Jarda via DM with short handoff message; 7-day observation window begins.

**Files:**
- `jarda-ai-start/README.md` (deploy notes, takedown plan)

**Steps:**
1. `git init` in `jarda-ai-start/` if not yet (handoff notes no repo yet).
2. Push to `mark-c4r/Jay-Z` GitHub repo (public repo name = privacy D2 decision).
3. Enable GitHub Pages on `main`, confirm deploy.
4. `curl https://mark-c4r.github.io/Jay-Z/ | bash scripts/privacy-audit.sh /dev/stdin` — final deployed-HTML privacy check.
5. Verify on iPhone Safari + Android Chrome + Chrome desktop.
6. DM Jarda with short normal-dude message + link.

**Tests:**
- Deployed URL renders identically to local on all three tested browsers
- View-source on deployed HTML: 0 denylist hits

**Depends on:** Slice 3

### Verify Gate (blocking v2b) — non-slice

After Slice 4 ship: 7-day observation window. Mark observes Jarda's engagement. **Decision signals:**
- v2b proceeds if: Jarda reaches Stop 3 within 3 days, OR runs a try-one, OR DMs a follow-up question
- v2b waits / adjusts if: Jarda opens briefly and bounces (stalls at Stop 2), OR doesn't open within 7 days (Mark DMs to check in, decide based on response)
- v2b cancels if: Jarda says v2a was enough

---

### Slice 5 (v2b): Stops 4, 5, 6 + their diagrams — downhill

**Demo:** All 6 stops populated. Stop 5 has 2 video blocks (Jack Roberts client + Jesse family). Rail shows all stops clickable.

**Files:**
- `jarda-ai-start/index.html` (replace Stop 4–6 placeholders with full content)
- `jarda-ai-start/assets/diagrams/stop-4-connector-scope.svg` + source
- `jarda-ai-start/assets/diagrams/stop-5-workflow-anatomy.svg` + source
- `jarda-ai-start/assets/diagrams/stop-6-habit-loop.svg` + source

**Steps:**
1. Pull Jeff Su connectors section (timestamps) → Stop 4 Block 1. Write short reading (Claire incident explanation) → Stop 4 Block 3.
2. Pull Jack Roberts client workflow 5-min (`jarda/transcripts/jack-roberts-cowork-course.txt`) → Stop 5 Block 1. Pull Jesse a16z family example 4-min (`jarda/transcripts/jesse-a16z-building-agents-at-home.txt`) → Stop 5 Block 2.
3. Pull Jesse "codify what works" 4-min (`jarda/transcripts/jesse-cognitive-revolution-try-this-at-home.txt`) → Stop 6 Block 1. Write short reading ("5 min every morning for a week") → Stop 6 Block 2.
4. Write 12 more branch drawers (Stops 4–6 × 4 branches).
5. Create 3 Excalidraw diagrams per style guide; export.

**Tests:**
- All 6 stops have content; rail shows all stops clickable + complete-markable
- Stop 5's 2-video layout stacks correctly on mobile

**Depends on:** v2a ship + verify-gate signal

### Slice 6 (v2b): Completion state — downhill

**Demo:** Check Stop 6's try-one checkbox → Triglav image + caption + one of 3 completion copies fades in below. Uncheck → hides.

**Files:**
- `jarda-ai-start/index.html` (completion block + fade animation)
- `jarda-ai-start/assets/hero-summit.jpg` (renamed from `hero-view.jpg`, role change)

**Steps:**
1. `git mv jarda-ai-start/assets/hero-view.jpg jarda-ai-start/assets/hero-summit.jpg` (role change; no re-processing — still EXIF-stripped at 213KB).
2. Implement listener: when `state.completed.blocks` includes `stop-6-try-one`, reveal block renders; when absent, hidden.
3. Fade-in animation: 400ms ease-out + `translateY(12px → 0)`.
4. Pick one of 3 completion-copy candidates (below) at build time. Sober voice sniff-test applied.
5. Image caption (serif italic, below image): "Slovenia · Triglav ridgeline, near the summit"

**Completion-copy candidates (pick one at build):**

A. *"That's the primer. You've got the shape. Try it on something real this week. If something breaks, the middle stops are where the answer usually is."*

B. *"Six stops done. You're now the one in your circle who set up Cowork correctly. From here it's practice — come back to any stop if you want to re-check something."*

C. *"Primer's done. What you do next is yours. If this page is still up in a few weeks, that's a bug — copy what you want before then."*

**Tests:**
- Check Stop 6 try-one → reveal fades in; uncheck → reveal hides (reversibility)
- Reader who deep-links to Stop 6 and checks directly still sees reveal

**Depends on:** Slice 5

### Slice 7 (v2b): Public appendix — downhill

**Demo:** Rail entry `Research · how these picks landed` (visually separated from spine by divider) clickable. Opens in-page appendix section with tool landscape + market map + "why these 6 stops." Callbacks from Stop 1 rationale and completion moment link to the appendix.

**Files:**
- `jarda-ai-start/index.html` (appendix section + callback text)

**Steps:**
1. Write tool landscape: Cowork vs Code vs Codex vs Gemini — ~250 words, sober voice, why Cowork for a beginner.
2. Write market map: Hesselberg, Ceranna, Zibura, Ben Love, Honest Guide, Rexby — 3–5 observations per competitor, ~400 words total. Names permitted (short-lived + public-research only per explicit user decision; CoS triangulation risk noted and accepted).
3. Write "why these six stops?" — ~150 words rationale + what was considered and dropped.
4. Wire rail entry to scroll + focus appendix section (separated from spine with horizontal divider per Gemini review).
5. Add one-sentence callback in Stop 1 rationale linking to appendix.
6. Add one-sentence callback in completion moment linking to appendix.

**Tests:**
- Click rail `Research` → scrolls + focuses appendix section
- Click Stop 1 callback and completion callback → both scroll to appendix
- Appendix is visually separated from spine stops (divider visible)

**Depends on:** Slice 6

### Slice 8 (v2b): Final polish + deploy — downhill

**Demo:** Full 19-item verification checklist passes (13 v2a items re-green + 6 v2b-specific items green); deployed URL updated; optional DM to Jarda noting v2 complete.

**Files:**
- `jarda-ai-start/index.html` (final copyedit pass)

**Steps:**
1. Voice grep pass on full document (now including appendix).
2. `bash scripts/privacy-audit.sh jarda-ai-start/index.html` — exit 0.
3. Lighthouse (mobile + desktop) — a11y ≥95.
4. Verify all 19 pre-ship items (13 v2a + 6 v2b-specific) + 6 post-ship friend-outcome items ready to observe.
5. Commit + push to `Jay-Z`; verify GitHub Pages rebuild.
6. (Optional) DM Jarda noting v2 is complete; no expectation.

**Tests:**
- All 19 pre-ship items green (13 v2a + 6 v2b)
- `curl https://mark-c4r.github.io/Jay-Z/ | bash scripts/privacy-audit.sh /dev/stdin` — exit 0

**Depends on:** Slice 7

## Existing Patterns

- **localStorage key reuse** — `jarda-ai-start/index.html:2157` defines `STORAGE_KEY = 'ai-start-onboarding-state'`. v2 keeps this exact key; schema migrates via fresh-state-on-load (no transform logic).
- **Privacy denylist discipline** — v1 slice plan `jarda-ai-start/docs/plans/2026-04-20-slice-4-privacy-readme-polish.md` established literal + regex + referral-URL patterns. v2 extends per Codex review with URL-encoded + case-variant + hyphen-variant forms, automated via `scripts/privacy-audit.sh`.
- **Hero image EXIF-stripping** — `jarda-ai-start/assets/hero-view.jpg` (Triglav, 213KB, EXIF-stripped) from v1 carries forward to v2 as `hero-summit.jpg` (git mv, role change only, no re-processing).
- **Inter + Fraunces italic typography** — v1 `<style>` tokens carry forward unchanged; v2 deploys Fraunces italic as the single editorial moment per stop (stop titles or rationale-line drop).
- **Tab-key a11y nav** — v1 uses logical tab order (verified via `grep -c "tabindex" jarda-ai-start/index.html`); v2 preserves with added skip-link at `#main`.

## What This Replaces

- `jarda-ai-start/index.html` (current 119KB v1) — full rewrite. Deleted: 5-tab SPA structure, 6 Wins pattern with chapter-timestamp rows, all `{your region}` / `{notable credential}` placeholder slots, Quick Magic cards, `Hi Jay Z` greeting, tab-button navigation.
- `jarda-ai-start/docs/plans/2026-04-20-onboarding-page-v1.md` — marked `status: superseded`, `superseded-by: 2026-04-21-v2-restructure.md` in frontmatter.
- `jarda-ai-start/docs/plans/2026-04-20-slice-[1-4]-*.md` — v1 slice plans remain as archaeology; frontmatter updated to `status: superseded`.

## No-Gos

- **No hero image at top** — Triglav only at completion state (this isn't a landing page).
- **No newsletter / RSS / analytics / signup / comments** — short-lived page.
- **No SEO / AEO / schema / image-SEO work** — won't rank, won't be live long enough.
- **No multi-language** — EN only.
- **No LocalStorage v3→v4 migration logic** — fresh state on load if old key present (per CoS review: over-investment for one reader).
- **No Lighthouse 100 chase** — ≥95 is the gate (over-investment flagged by CoS).
- **No discoverability notes in public appendix** — deferred to v2.5 (scope creep risk).
- **No Glossary / All prompts / About-this-page sidetrips** — rail stays focused on spine + one appendix entry.
- **No domain assumptions in branch chip labels** — `Personal` not `Personal · kids + school`. Examples live inside drawer content only.
- **No emojis anywhere** — for landing pages, not instructional content.
- **No "while I'm here" scope creep during v2a** — Stops 4–6 are placeholders only. No sneaking v2b content into v2a.

## Verification Commands

Pre-ship for v2a (run after Slice 3, again after Slice 4 on deployed URL):

```bash
# 1. Voice sniff
grep -En '!|\bamazing\b|\bpowerful\b|\btruly\b|\bexciting\b|let'"'"'s dive in|\btogether\b|just for you' jarda-ai-start/index.html

# 2. Privacy audit (full variants)
bash scripts/privacy-audit.sh jarda-ai-start/index.html

# 3. Branch labels clean
grep -cE 'Personal.*kids|Creative.*photo|Client.*business|your family' jarda-ai-start/index.html

# 4. StorageKey preserved
grep -c "ai-start-onboarding-state" jarda-ai-start/index.html

# 5. Hero rename complete (no more hero-view.jpg references)
! grep -q "hero-view\.jpg" jarda-ai-start/index.html

# 6. Diagram count matches phase
test $(ls jarda-ai-start/assets/diagrams/*.svg 2>/dev/null | wc -l) -ge 3  # v2a: 3; v2b: 6

# 7. Excalidraw source committed
test $(ls jarda-ai-start/excalidraw-source/*.excalidraw 2>/dev/null | wc -l) -ge 3

# 8. Private appendix separate
test -d jarda/jarda-private/ && test $(ls jarda/jarda-private/*.md | wc -l) -ge 2

# 9. Gitignore entry
grep -q "jarda-private" jarda/.gitignore

# 10. Lighthouse a11y
npx lighthouse https://mark-c4r.github.io/Jay-Z/ --only-categories=accessibility --output=json --quiet | jq '.categories.accessibility.score >= 0.95'

# 11. Mobile viewport (manual)
# Open on iPhone Safari at 375px — confirm sticky top + drawer + sticky bottom + no horizontal scroll

# 12. Deployed HTML privacy final
curl -sL https://mark-c4r.github.io/Jay-Z/ | bash scripts/privacy-audit.sh /dev/stdin
```

## Reviewer findings — explicit decisions against

Documented here so future sessions can audit judgment calls:

- **Lighthouse 100 → ≥95**: accepted CoS "over-investment" framing.
- **Excalidraw source commits**: kept despite CoS flag. Per Codex — editability worth minor repo weight.
- **Competitor names in public appendix**: user decision stands (short-lived + public-materials-only research). CoS triangulation risk noted and accepted.
- **Visual signature element**: deferred to build time explicitly (Slice 1 — builder explores 2–3 options in Stop 1 implementation, picks one, applies systematically).
- **Voice cadence expansion** (per Chief Designer): drafted inline during v2a build, not pre-build. One sample + positive-markers + anti-markers is sufficient scaffolding.
- **Appendix discoverability (AEO/SEO)**: deferred to v2.5.
- **Sidetrips (Glossary / All prompts / About)**: removed from v2 scope entirely.
- **v3→v4 localStorage migration logic**: skipped per CoS. Fresh-state-on-load instead.

## Brainstorming artifacts (reference)

Under `~/Coding/jarda/.superpowers/brainstorm/50244-1776751572/content/`:
- `stop-pattern.html` — per-stop wireframe (desktop)
- `course-outline.html` — 6 stops + block compositions
- `progress-nav.html` — top bar + expanded rail + bottom nav
- `mobile.html` — 375px viewport + drawer (note: hamburger position corrected to drawer-side in spec)
- `voice-sample.html` — 3 voice registers + v1 anti-pattern
- `running-summary.html` / `design-complete-v2.html` — running decision log

## Post-approval workflow

1. Approve this contract (ExitPlanMode or equivalent)
2. Copy this spec to `jarda-ai-start/docs/plans/2026-04-21-v2-restructure.md` (status: active)
3. Mark v1 plan + 4 slice plans `status: superseded` with `superseded-by: 2026-04-21-v2-restructure.md`
4. Invoke `superpowers:writing-plans` to produce an executable v2a slice plan (detailed PIV commands per slice)
5. Build v2a slice-by-slice, verifying each before advancing
6. Ship v2a → 7-day verify gate with Jarda → decide on v2b (proceed / adjust / cancel)
