---
ticket: jarda-ai-start/cluster-3-prerequisites
status: superseded
superseded-by: 2026-04-21-round-2-master.md
appetite: S
risk_score: 2
project: jarda-ai-start
updated: 2026-04-21
files:
  - index.html
intended-destination: docs/plans/2026-04-21-cluster-3-prerequisites.md
note: >
  Plan mode is active; Write is restricted to this session plan file. After
  approval, copy this document verbatim to the intended-destination path and
  commit.
---

# Cluster 3 — Prerequisites / Stop 0 (Jarda AI-Start v2b)

## Problem

The page jumps into "Stop 1: what Cowork is" without explaining how Jarda
arrives in a position to use it. There is no mention of a Claude account,
the plan tier that unlocks Cowork/Code/Projects/Connectors/Skills, or the
voice layer (WisprFlow) that makes long prompting ergonomic. User feedback,
verbatim: *"at what point should Jarda create his Claude? and how he should
set it up? At what point he should get his WisprFlow and how to effectively
use it?"*

Outcome we're after: a reader who lands cold can finish the prerequisite
section in under 2 minutes, knows exactly which plan to pay for, knows
what WisprFlow is and why to pair it, and can start Stop 1 with both
accounts signed in. Measurement: qualitative reader-review pass ("would a
new reader know what to sign up for after this section alone?").

## Verified Assumptions

| Claim | Verify | Verified At |
|---|---|---|
| `STOPS[]` at `index.html:1894-1901` has exactly 6 entries, all `populated: true`. | `grep -nE "{ n: [0-9], title:" /Users/profile_1/Coding/jarda/jarda-ai-start/index.html` | 2026-04-21 |
| Top-bar renders `Stop N of 6` at `index.html:1284` and `stop-meta` divs at 1306/1380/1454/1527/1605/1708 hardcode `Stop N of 6`. | `grep -n "Stop [1-6] of 6" /Users/profile_1/Coding/jarda/jarda-ai-start/index.html` | 2026-04-21 |
| Existing rail sidetrip pattern lives at `index.html:1296-1298` as an `<ol class="rail-sidetrips">` sibling to `.rail-stops`, with one entry `<a href="#research" class="sidetrip-link">Research · how these picks landed</a>`. | `grep -n "rail-sidetrips\\|sidetrip-link" /Users/profile_1/Coding/jarda/jarda-ai-start/index.html` | 2026-04-21 |
| Progress bar formula at `index.html:1951-1955`: `totalBlocks = STOPS.reduce(...)`, `completedBlocks = state.completed.blocks.length`, `pct = 100 * completedBlocks / totalBlocks`. Anything NOT in `STOPS[].blocks` is automatically excluded. | `grep -n "totalBlocks\\|completedBlocks\\|tb-fill" /Users/profile_1/Coding/jarda/jarda-ai-start/index.html` | 2026-04-21 |
| Stop 1 section anchor is `<section id="stop-1">` at `index.html:1304` — new `<section id="setup">` must precede it in DOM order. | `grep -n "id=\"stop-1\"" /Users/profile_1/Coding/jarda/jarda-ai-start/index.html` | 2026-04-21 |
| No prior `privacy-audit` / `voice-grep` script exists; cluster-3 verification will use inline `grep` invocations rather than script names. | `ls /Users/profile_1/Coding/jarda/jarda-ai-start/scripts/ 2>&1 \| grep -c .` returns non-zero-exit (dir missing). | 2026-04-21 |
| **External tier facts (not grep-able):** Claude Pro = $20/mo includes Cowork, Code, projects, connectors, skills. Free tier excludes Cowork/Code. WisprFlow free tier ~2k words/week, Pro ~$12/mo. | Confirmed in prompt; copy will say "around twenty dollars a month" and "around twelve dollars" — no exact figures locked. | 2026-04-21 |

No yellow/orange rows. All claims green.

## Shape Decision

**Option D — "Setup" rail entry, NOT numbered as a stop.**

Why D over A/B/C:
- **A (Stop 0 in `STOPS[]`)**: breaks the "Stop N of 6" convention in the
  top bar and the per-stop `stop-meta` divs; would require touching 8+
  labelled strings for cosmetic gain. Also counts Setup toward
  `totalBlocks`, inflating the progress bar with a one-block pre-req.
- **B (plain sidetrip)**: visually indistinguishable from the "Research"
  sidetrip; setup is coursework, research is side material. Readers
  would skip it.
- **C (prepend to Stop 1)**: dilutes Stop 1's purpose ("what Cowork is");
  Jarda's feedback was precisely that Stop 1 *already* feels like it
  starts mid-conversation. Pushing prereqs into Stop 1 repeats the same
  failure.
- **D (Setup rail entry, separate `<section id="setup">` before Stop 1)**:
  preserves the 6-stop counter, visually signals "this comes first" by
  sitting ABOVE Stop 1 in the ordered rail, reads as coursework (not a
  sidetrip), and stays out of `STOPS[]` so the progress bar only counts
  the 6 real stops. Minimum disruption for maximum legibility.

Structural notes:
- New `<section id="setup">` inserted between `<aside>` rail and
  `<section id="stop-1">` in `<main>`.
- New rail entry rendered as a **static `<li>` in the existing `<ol
  class="rail-stops">`**, prepended before the JS-populated
  `STOPS[]`-driven list. Alternative: add a second static
  `<ol class="rail-setup">` list above `.rail-stops`. Executor picks the
  lower-diff option after reading the `renderRail()` DOM-replacement
  logic at `index.html:1915-1927` (which does `ol.innerHTML = ...` and
  would wipe any static children of `.rail-stops`). **Assumption: a
  second static `<ol class="rail-setup">` above `.rail-stops` is the
  safer path** because `renderRail()` currently replaces the full
  innerHTML of `.rail-stops`.
- Setup link navigates to `#setup`; does NOT use `data-stop` attribute
  (so `onStopClick` at `index.html:1929` won't mutate
  `state.currentStop`).
- Setup section contains: (1) prose reading block, (2) a single
  "install both, sign in" progress-anchor checkbox with id like
  `setup-installed` that is NOT registered in `state.completed.blocks`
  (pure visual anchor — survives via `localStorage` only if we wire it,
  or is ephemeral if we don't). **Assumption: keep it ephemeral for
  simplicity**; v2c can add persistence if needed.
- No URL to `claude.com` or `wisprflow.ai` per the voice/privacy rules
  the rest of the page follows.

## Acceptance Criteria

- [ ] `<section id="setup">` exists in `index.html` before
  `<section id="stop-1">`.
- [ ] Rail contains a Setup entry above the Stop 1 rail entry, rendered
  such that subsequent `renderRail()` calls do not wipe it.
- [ ] Setup link `href="#setup"` navigates to the section; clicking it
  does NOT change `state.currentStop`.
- [ ] Setup section contains prose of ~140-180 words, sober voice matching
  Stop 1 register, with the final draft below as the starting text.
- [ ] Copy mentions: Claude Pro ≈ $20/mo, Cowork/Code/projects/connectors/
  skills all included in Pro, free tier excludes Cowork/Code, WisprFlow
  free tier ~2k words/week, WisprFlow Pro ~$12/mo.
- [ ] No URLs to `claude.com` or `wisprflow.ai` anywhere in the Setup
  section.
- [ ] No `{your region}` / `{notable credential}` slot placeholders or
  any other `{...}` template slots in Setup prose.
- [ ] Privacy audit passes: no PII, no location inferences, no
  personalised addressing — verified by inline grep (see
  Verification Commands).
- [ ] Voice grep passes: no banned hype words — verified by inline grep.
- [ ] Progress bar at 0% completion still reflects `0/totalBlocks` across
  the 6 real stops; Setup's checkbox (if added) is NOT counted.
- [ ] Top-bar still reads "Stop N of 6" for the 6 real stops; Setup does
  not appear in top-bar labelling.
- [ ] Formal reviewer pass on Setup prose, same pattern as Slice 3
  (reader-review: does someone cold know what to sign up for?).

## Slices

**Slice 1 — Setup section + rail entry + prose** (~60-80 LOC, S appetite, ≤45 min)

Tasks:
1. Add second `<ol class="rail-setup">` above `<ol class="rail-stops">`
   in `<aside id="rail">` (around `index.html:1292`) with one `<li>`
   entry: `<a href="#setup" class="sidetrip-link setup-link">Setup ·
   Before you open the chat</a>`. Class shares `sidetrip-link` styling;
   `setup-link` modifier is for any future specific styling.
2. Add `<section id="setup" class="setup" aria-labelledby="setup-title">`
   immediately before `<section id="stop-1">` at `index.html:1304`. Use
   a simplified `.stop`-like skeleton but without `stop-meta`
   (no "Stop N of 6"). Include:
   - `<h2 id="setup-title">Before you open the chat</h2>`
   - `<p class="setup-rationale">` containing the final-draft prose
     below, rendered as either a single paragraph or two paragraphs
     matching the draft's structure.
   - `<label class="setup-checkbox"><input type="checkbox" id="setup-installed"> Both installed, signed in</label>`
     — no listener, no `state.completed.blocks` registration.
3. Add minimal CSS if needed to make `.setup` look like a "lighter"
   stop: smaller top margin, same typography family as `.stop-header`,
   no `.block`-style card. Prefer reusing existing `.stop-rationale`
   typography for the prose.
4. Smoke verify: load `index.html` locally, confirm Setup section
   appears above Stop 1, rail Setup link scrolls to it, Stop 1's "Stop
   1 of 6" label unchanged, progress bar at 0%.

Dependencies: none (no other cluster blocks this).

Demo: Open `index.html`, see rail with Setup entry above "1 · Start
here", click it, land on the Setup section. Scroll down — Stop 1 is
unchanged. Top-bar reads "Stop 1 of 6" (not "Stop 0 of 7").

## Final Draft (copy for executor to paste, ~150 words)

> Two one-time steps before the primer is useful.
>
> Sign up at Claude and pick **Pro** — around twenty dollars a month, pay for one, cancel any time. Pro includes everything this page describes: Cowork, Code, projects, connectors, skills. The free tier does not. Max, Team, and Enterprise are the same product with higher rate limits — save those for later.
>
> The second step is a voice layer. **WisprFlow** is a keyboard overlay that writes what you say, anywhere you can type. A free tier of about two thousand words a week is enough to try. Pro runs around twelve dollars a month once it earns its keep. The reason to pair it with Cowork is obvious the first time you dictate a three-paragraph brief between two shoots instead of typing it.
>
> Install both. Sign in. Nothing else yet. The primer starts where the blank chat window does.

Word count: ~150. Trimmed from the content agent's 180 by dropping
"claude.com" URL (handled as "Sign up at Claude") and tightening the
Max/Team sentence to one clause.

## No-Gos

- **No affiliate URLs** — no `ref=`/`via=` tracking, no referral links.
- **No hardcoded screenshots** of the Claude signup or WisprFlow install
  flows — vendor UIs change; screenshots rot.
- **No step-by-step signup walkthrough** — same reason. "Sign up at
  Claude" is enough; Jarda can handle a signup form.
- **No pricing precision** — "around twenty dollars" and "around
  twelve" are deliberate; exact figures go stale and don't match
  regional pricing.
- **No rephrasing as a sales pitch** — sober voice, match Stop 1's
  register.
- **No adding Setup to `STOPS[]`** — keeps the 6-stop counter intact
  and keeps the progress bar clean.
- **No persistence on the install checkbox** (v2b scope). If a later
  cluster wants it, that's a separate ticket.
- **No cross-link to a deferred "Troubleshooting install"** page. Out
  of scope.

## Verification Commands

```bash
# 1. Setup section exists and sits before stop-1
grep -nE "id=\"(setup|stop-1)\"" /Users/profile_1/Coding/jarda/jarda-ai-start/index.html

# 2. Rail Setup entry exists, links to #setup, does not use data-stop
grep -n "setup-link\\|href=\"#setup\"" /Users/profile_1/Coding/jarda/jarda-ai-start/index.html

# 3. STOPS[] still has exactly 6 populated entries (unchanged)
grep -cE "{ n: [1-6], title:" /Users/profile_1/Coding/jarda/jarda-ai-start/index.html
# Expected: 6

# 4. No URLs to claude.com or wisprflow.ai
grep -nE "claude\\.com|wisprflow\\.ai" /Users/profile_1/Coding/jarda/jarda-ai-start/index.html
# Expected: 0 matches

# 5. No template slots left in Setup section (scoped grep)
awk '/<section id="setup"/,/<\\/section>/' /Users/profile_1/Coding/jarda/jarda-ai-start/index.html | grep -cE '\\{[a-z ]+\\}'
# Expected: 0

# 6. Voice grep — no banned hype words in Setup section
awk '/<section id="setup"/,/<\\/section>/' /Users/profile_1/Coding/jarda/jarda-ai-start/index.html | grep -iE "seamless|effortless|unleash|supercharge|game-changer|unlock the power|best-in-class"
# Expected: 0 matches
```

All six must return the expected values for the slice to pass verification.
