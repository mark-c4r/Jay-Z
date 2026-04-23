---
ticket: jarda-ai-start/cluster-5-youtube-chapters
status: superseded
superseded-by: 2026-04-21-round-2-master.md
appetite: M
risk_score: 4
project: jarda-ai-start
updated: 2026-04-21
files:
  - jarda/scripts/fetch-chapters.sh
  - jarda-ai-start/assets/chapters.json
  - jarda-ai-start/index.html
---

# Cluster 5 — YouTube Chapters Integration (v2b.1)

## Problem

Current Stop 1–6 facades each ship 4 hand-curated highlight lines. User observation:

> "For the click-to-jump sections — we don't have to always limit ourselves just to 4 options; also, maybe try to leverage the chapter names and timestamps from youtube, those might be better in many cases than the transcripts themselves."

Two sub-problems:
1. **Accuracy** — Hand-authored timestamps may drift from the actual beat creators marked. Creators' own chapter boundaries are ground truth for "what happens when" in the video.
2. **Breadth** — 4 highlights is arbitrary. Some stops (e.g., Jack Roberts 22:58–25:59 "connectors" block) naturally cover 4 distinct sub-topics; others (Jesse Genet a16z 13:53–16:30) cover 1. Locking at 4 hides breadth signal.

Outcome: richer, more accurate click-to-jump highlights without losing the sober editorial voice that calibrates the page. Measured by: per-stop highlight count varies (3–8, not uniform 4), timestamps align within ±15s of real creator chapter boundaries, voice audit (no algorithm-bait phrasing leaks through).

## Verified Assumptions

| # | Claim | Source / Verify | State |
|---|-------|-----------------|-------|
| 1 | All 4 videos have published chapters | `yt-dlp --skip-download --print "%(chapters)j" <vid>` — run per research findings in intake | Verified (content research) |
| 2 | Jeff Su `z9rdrNrkvDY` = 9 chapters, 19m06s | Intake research | Verified |
| 3 | Jack Roberts `cNf7uVff11Y` = 46 chapters, 65m18s | Intake research | Verified |
| 4 | Jesse Genet a16z `yiJOTCRVWjc` = 8 chapters, 54m02s | Intake research | Verified |
| 5 | Jesse Genet Cog Rev `aFQskhdR3RQ` = 22 chapters, 126m23s | Intake research | Verified |
| 6 | Stop 6 segment 40:09–43:30 intersects Cog Rev "Context, models, and privacy (40:57)" chapter | Extracted chapter list from intake | Verified |
| 7 | Visual threshold: 3–8 highlights read cleanly, 9–15 need grouping, 16+ overwhelm | Agent 2 research (cited in intake) | Verified |
| 8 | Browser cannot run yt-dlp — chapter fetch must be author-time | Architectural constraint (no Node/yt-dlp runtime in static page) | Verified |
| 9 | Chapter titles from creators are public YouTube metadata — no privacy risk | NA — YouTube chapters are publicly displayed on video pages | Verified |
| 10 | Some creator chapter titles are SEO-chirpy and would violate voice calibration | Intake analysis + general YouTube patterns | Verified (requires curation pass) |

## Shape Decision — Path A (Middle Ground)

Three paths were weighed:

- **Path A (chosen)**: Build `jarda/scripts/fetch-chapters.sh` in umbrella repo. Pull chapters for all 4 videos into a local JSON artifact. USE that JSON as the authoring source of truth to re-author the highlights in Stop 1–6 — more accurate timestamps, up to 8 per stop where breadth warrants. Keep sober voice. **No runtime JSON fetch.** Ship only the re-authored `index.html`.
- Path B (rejected): Full runtime fetch — commit `assets/chapters.json`, JS filters chapters by facade range, renders them directly. Risks voice drift (raw chapter titles are often clickbait); adds 40 LOC JS + fetch failure modes to debug.
- Path C (rejected for v2b.1): Hybrid — curated list primary, collapsible "full chapter list" secondary. Adds UI affordance we haven't designed; scope creep.

**Why Path A:** voice is load-bearing for the page. The editorial calibration (sober, no-hype) is more valuable than automation breadth right now. Chapters as a data source for authoring gives us the accuracy win without the voice risk. Path B can be revisited once voice is stable and we want power-user nav.

### Shape sketch

```
jarda/scripts/fetch-chapters.sh   (umbrella, NOT shipped to public repo)
  └── runs yt-dlp --skip-download --print "%(chapters)j" on 4 video IDs
      → writes jarda/scripts/chapters.json (umbrella-only artifact, gitignored in public repo)

Author (human + Claude) reads chapters.json
  → rewrites <ul class="facade-highlights"> inside each .yt-facade
  → timestamps align to chapter starts (±15s tolerance for narrative flow)
  → 3–8 items per facade based on how many chapters intersect the segment
  → voice pass: paraphrase any SEO-y chapter titles into sober phrasing
```

No new runtime dependencies. No new JS. Only `index.html` changes in the public repo.

## Acceptance Criteria

- [ ] `jarda/scripts/fetch-chapters.sh` exists in the umbrella repo, runs `yt-dlp --skip-download --print "%(chapters)j"` for all 4 video IDs, writes `jarda/scripts/chapters.json`
- [ ] `jarda/scripts/chapters.json` exists locally with `{videoId: {duration, chapters: [{start, title}]}}` shape for all 4 videos
- [ ] `jarda-ai-start/.gitignore` (or equivalent) excludes any chapter artifact paths — NOT shipped to public repo for Path A
- [ ] Each Stop 1–6 facade's `<ul class="facade-highlights">` has been reviewed against chapter data and re-authored
- [ ] Highlight timestamps fall within ±15s of actual creator chapter boundaries (verified by spot-checking 3 facades against source chapters)
- [ ] At least one stop has **more than 4** highlights (proof that we've broken the arbitrary 4-cap)
- [ ] No stop has **more than 8** highlights (visual threshold)
- [ ] No stop has **fewer than 3** highlights (minimum useful nav)
- [ ] Voice audit: zero SEO-chirpy phrasing leaked through (no "The 10 Best Secrets", no "You Won't Believe", no emoji from source titles unless sober editorial use); each label reads like editorial sidebar copy, not algorithm bait
- [ ] Cluster 2 Bug #5 (click-to-jump handler) ships first or in the same sweep — chapter-timed clicks are useless without the handler fix
- [ ] Lighthouse a11y ≥ 0.95 (no regression from chapter re-authoring; same `<ul><li><button>` structure)
- [ ] Page weight delta < 2KB (text-only changes in `index.html`)

## Slices

### Slice 1 — Fetch script + local chapters.json (downhill 🔽)

- **Demo:** `bash jarda/scripts/fetch-chapters.sh` produces `jarda/scripts/chapters.json` with all 4 videos' chapter data
- **Files:** `jarda/scripts/fetch-chapters.sh` (new, ~30 LOC), `jarda/scripts/chapters.json` (generated artifact, umbrella-only), `jarda/.gitignore` (confirm chapters.json tracked in umbrella)
- **Tests:** Manual — run script, inspect JSON, spot-check one chapter against live YouTube video page
- **Depends:** yt-dlp installed locally (already present per intake research)
- **Rabbit holes avoided:** No packaging into Node script; bash + yt-dlp + jq is enough. No remote CI run; this is an author-time tool for one person.

### Slice 2 — Re-author highlights per stop using chapter data (uphill 🔼 — voice judgment)

- **Demo:** Open `jarda-ai-start/index.html` in browser; each Stop 1–6 facade shows 3–8 highlights with timestamps matching creator chapter boundaries; voice reads consistent with current page tone
- **Files:** `jarda-ai-start/index.html` (edits to 6 facade blocks)
- **Tests:**
  - Spot-check: for 3 random facades, `grep` current hand-authored timestamps against chapters.json — verify within ±15s
  - Voice audit: read every new highlight label aloud; flag any that sound like clickbait or SEO
  - Count audit: `grep -c '<li>' inside each facade-highlights block` returns 3–8; at least one returns > 4
- **Depends:** Slice 1 (chapters.json exists); Cluster 2 Bug #5 click-handler fix (same sweep or prior)
- **Per-video curation plan:**
  - **Stop 1–3 (Jeff Su, 0:00–19:06):** Map segments to subset of 9 chapters. Stop 1 = chapters at 0:00 + 2:19 (intro + settings); Stop 2 = chapter at 14:26 (Cowork Projects) + nearby; Stop 3 = chapter at 6:14 (Persistent Memory). Candidate for 4–6 highlights each.
  - **Stop 4 (Jeff Su connectors 8:44):** Single chapter "Tools & Connectors" — expand with adjacent 10:38 "Claude Skills" for breadth → 2–3 highlights within Jeff's segment + pivot to Jack Roberts if segment spans
  - **Stop 5a (Jack Roberts 22:58–25:59):** 46-chapter video; range-filter finds ~4 chapters in this window (Connectors Overview, Google Calendar Setup, Other Connectors, Morning Brief) — perfect 4, possibly 5 with nearby
  - **Stop 5b (Jesse Genet a16z 13:53–16:30):** Only 1 chapter intersects ("Personalized lesson plans" at 11:00). Either keep hand-authored micro-timestamps OR extend segment to include chapter at 18:00 — decide at author-time
  - **Stop 6 (Jesse Genet Cog Rev 40:09–43:30):** Chapter "Context, models, and privacy (40:57)" intersects. Plus nearby "Onboarding agents like employees Part 1 (31:03)" if segment extends — likely 2–4 highlights
- **Rabbit holes avoided:** Not rebuilding the segment ranges themselves (that's Cluster 4 territory); not introducing chapter-level nested nav.

## No-Gos

- **No runtime chapter fetching.** `chapters.json` stays umbrella-only; public repo ships only re-authored `index.html`.
- **No raw SEO-chirpy titles.** If a creator chapter title is clickbait, paraphrase to match the page's sober editorial voice. Chapter data is source, not literal label.
- **No more than 8 highlights per facade.** Visual threshold is real; don't dump 46 chapters into Jack Roberts' stop.
- **No fewer than 3 highlights per facade.** Even if a segment only intersects 1 chapter, pad with adjacent chapters or break the 4-cap floor in the other direction (3 is fine).
- **No segment re-shaping.** Cluster 5 uses existing Stop 1–6 segment ranges. Changing segment ranges is out of scope (would re-open Cluster 4 decisions).
- **No new JS.** Path A is author-time only.
- **No commits to public repo of chapter JSON.** Umbrella artifact only.
- **No coupling to Cluster 1/3 scope.** This ticket is independent of those clusters except for the Cluster 2 Bug #5 click-handler dependency.

## Verification Commands

Run at PIV time (before ship):

```bash
# Slice 1 verification
test -x jarda/scripts/fetch-chapters.sh || { echo "MISSING fetch script"; exit 1; }
test -f jarda/scripts/chapters.json || { echo "MISSING chapters.json"; exit 1; }
jq 'keys | length' jarda/scripts/chapters.json  # expect 4
jq '."z9rdrNrkvDY".chapters | length' jarda/scripts/chapters.json  # expect 9
jq '."cNf7uVff11Y".chapters | length' jarda/scripts/chapters.json  # expect 46
jq '."yiJOTCRVWjc".chapters | length' jarda/scripts/chapters.json  # expect 8
jq '."aFQskhdR3RQ".chapters | length' jarda/scripts/chapters.json  # expect 22

# Slice 2 verification — public repo clean of artifact
! test -f jarda-ai-start/assets/chapters.json || { echo "LEAKED chapters.json to public repo"; exit 1; }
! grep -rn "chapters.json" jarda-ai-start/index.html || { echo "LEAKED runtime fetch"; exit 1; }

# Highlight count audit per facade
python3 - <<'PY'
import re, sys
html = open('jarda-ai-start/index.html').read()
blocks = re.findall(r'<ul class="facade-highlights">(.*?)</ul>', html, re.DOTALL)
fails = []
if len(blocks) < 6:
    fails.append(f"expected ≥6 facade-highlights blocks, got {len(blocks)}")
has_over_four = False
for i, b in enumerate(blocks, 1):
    n = b.count('<li>')
    if n < 3 or n > 8:
        fails.append(f"facade {i}: {n} highlights (want 3–8)")
    if n > 4:
        has_over_four = True
if not has_over_four:
    fails.append("no facade has >4 highlights — breadth proof missing")
if fails:
    print("FAIL:"); [print("  ", f) for f in fails]; sys.exit(1)
print("PASS highlight count audit")
PY

# Timestamp spot-check (manual, 3 facades): for each, compare <button data-t=...> values to chapters.json
# This is a judgment check; automate if we do this more than twice.

# Lighthouse a11y
npx -y @lhci/cli@0.14.x autorun --collect.url=file://$(pwd)/jarda-ai-start/index.html --assert.assertions.categories:accessibility=0.95
```

## Dependencies / Sequencing

- **Cluster 2 Bug #5** (click-to-jump handler) must ship first or in the same sweep. Chapter-accurate timestamps are worthless if the click doesn't seek. Recommend: land Cluster 2 first, then Cluster 5 Slice 1, then Slice 2.
- `yt-dlp` already present locally.
- No other cluster dependencies.

## Risk Score Breakdown (4/8)

- Novelty: 1 (new author-time script, but trivial shape; no new runtime)
- Reversibility: 0 (text-only edits to `index.html`; git revert works)
- Dependencies: 2 (depends on Cluster 2 Bug #5 for the click handler; yt-dlp; voice judgment)
- Interface uncertainty: 1 (voice audit is subjective — hence the audit step)

Total: 4. Medium risk → Clarify → Explore → Contract (this doc). No spike needed; yt-dlp output is known from intake research.

## Cross-Model Review

Risk score 4 hits the MANDATORY threshold (≥4). Before approving this plan for execute:

- [ ] Codex adversarial review on the shape (Path A vs B vs C, voice-drift risk, curation judgment, Cluster 2 sequencing)
- [ ] Fold findings, run verification round if any folds modify structure

Gemini review not triggered (no UI/design shape change beyond list length).

## Open Questions (resolve at Slice 2 author-time)

1. Stop 5b — extend segment to include "5 to 11 agents (18:00)" chapter, or keep tight 13:53–16:30 with 3 hand-authored micro-timestamps? Author judgment at re-authoring pass.
2. Stop 6 — include the "Onboarding agents like employees Part 1 (31:03)" chapter even though 31:03 falls outside the 40:09–43:30 segment? Probably not — respect the segment boundary; Cluster 4 can widen segments if needed.
3. Jack Roberts Stop 5a — exactly which 4–5 of the ~4 intersecting chapters land in the final list? Author call based on which read cleanest in sober voice.

These are author-time micro-decisions, not blockers for shape approval.
