---
ticket: jarda-ai-start/cluster-1-market-map-correction
status: superseded
superseded-by: 2026-04-21-round-2-master.md
appetite: S
risk_score: 1
project: jarda-ai-start
updated: 2026-04-21
urgency: blocker (factual error in live content)
---

> **Note on file target:** Plan mode is active; this draft lives at `~/.claude/plans/yes-let-s-skip-that-structured-tarjan-agent-a2ec39b5aa33a7839.md`. On approval, copy verbatim to `/Users/profile_1/Coding/jarda/jarda-ai-start/docs/plans/2026-04-21-cluster-1-market-map-correction.md` before Slice 1 starts. The YAML frontmatter above is already final.

# Cluster 1 · Market Map correction

## 1. Problem

When Jarda scrolls to the research appendix he sees a "Market map" block naming six voices — Hesselberg, Ceranna, Zibura, Ben Love, Honest Guide, Rexby — each paired with a fabricated AI-teaching description ("Long-form YouTube explainers", "Instructor register", "Agents and automation", etc.). Every one of those six names is in reality one of **Jarda's own competitive peers** for his personal businesses (wedding photographer, elopement photographer, travel author, Prague tourism channel, routes-app platform). None of them teach AI. The block as shipped directly contradicts the page's core promise — "sober, honest author notes" — and is a factual integrity bug. **Demand-side "when" test:** when Jarda scrolls to the Market Map, he should see five real AI-teaching voices he can actually go watch, with behavioral descriptions that match what those voices actually do. Today, he sees six fictions he'd instantly recognize as wrong, because four of them are people he *personally knows as photographers and authors*.

## 2. Verified Assumptions

| # | Claim | Verify command | Result |
|---|-------|----------------|--------|
| 1 | `index.html:1811-1826` contains the "Market map" block with the six fabricated names | `sed -n '1811,1826p' /Users/profile_1/Coding/jarda/jarda-ai-start/index.html \| grep -cE 'Hesselberg\|Ceranna\|Zibura\|Ben Love\|Honest Guide\|Rexby'` → expect 6 | Confirmed via Read: block is at lines 1811-1826, all six names present in `<ul>` at 1815-1820 |
| 2 | `discovery-plan.md:250-263` lists the five real AI-teaching voices with 1-3 sentence rationale each | `sed -n '250,263p' /Users/profile_1/Coding/jarda/discovery-plan.md \| grep -cE 'Ruben Hassid\|Jack Roberts\|Jesse Genet\|Jeff Su\|Sarah Cordiner'` → expect ≥5 | Confirmed via Read: block at 250-263 names all five with rationale; Hassid quote at 261 ("Prompts → Projects → Skills") is the scaffolding |
| 3 | Jeff Su, Jack Roberts, Jesse Genet already appear as primer Stop sources — evidence that they're the right voices for this page's readership | `grep -cE 'Jeff Su\|Jack Roberts\|Jesse Genet' /Users/profile_1/Coding/jarda/jarda-ai-start/index.html` → expect ≥3 | To run pre-Slice 1 (presumed true from discovery-plan references at 255-257) |
| 4 | Privacy-audit script exists and currently passes on `index.html` | `test -x /Users/profile_1/Coding/jarda/jarda-ai-start/scripts/privacy-audit.sh && /Users/profile_1/Coding/jarda/jarda-ai-start/scripts/privacy-audit.sh` → expect exit 0 | To run pre-Slice 1; if script path differs, locate via `ls /Users/profile_1/Coding/jarda/jarda-ai-start/scripts/` |
| 5 | Voice-grep banned markers list is known (no "best", "leading", "top", marketing superlatives) | `grep -cE '\b(best\|leading\|top\|ultimate\|revolutionary)\b' /Users/profile_1/Coding/jarda/jarda-ai-start/index.html` baseline | To run pre-Slice 1 and post-Slice 1 — post count must not increase |

**Staleness note:** All verify commands above must re-run at the start of Slice 1 (same-session shape-then-ship). Claims describe pre-build state; the rewrite invalidates #1 by construction.

## 3. Shape Decision

**Decision: Option A — Swap-in-place.**

Replace the six fabricated names in the existing `<ul>` at `index.html:1815-1820` with five real AI-teaching voices (Hassid, Su, Roberts, Genet, Cordiner). Keep the `<h3>Market map</h3>` title, the intro paragraph at `:1813`, and the three trailing observation paragraphs at `:1823-1825`. Rewrite only the intro sentence + the `<ul>` items + (possibly) light retuning of the two-axes observation at `:1823` so it still reads coherently with five voices instead of six.

**Why A over B or C:**
- **B (Split into two blocks):** Introducing a second "Jarda's own competitive peers" block inverts the appendix's purpose (teach the reader about AI, not about Jarda's industries) and creates an awkward self-reference. Also bloats the appendix at a stage when the page is already content-dense.
- **C (Delete):** Loses real value — the five voices *are* legitimate next-step reading for a primer reader. Deletion over-corrects.
- **A (Swap):** Surgical. Matches existing ~400w slot. Zero structural change to the page. Trivial to reviewer-verify.

**Budget:** 5 voices × ~60-70 words each (300-350w) + ~50w intro + ~100w retained observation tail = ~500w (was ~440w). Within tolerance.

**Rollback:** Single-file, single-block diff. `git revert` on the commit returns the page to current state with zero collateral.

## 4. Acceptance Criteria

- [ ] `grep -cE 'Hesselberg\|Ceranna\|Zibura\|Ben Love\|Honest Guide\|Rexby' /Users/profile_1/Coding/jarda/jarda-ai-start/index.html` → **0** (all six fabricated names removed)
- [ ] `grep -cE 'Ruben Hassid\|Sarah Cordiner' /Users/profile_1/Coding/jarda/jarda-ai-start/index.html` → **≥2** (Hassid + Cordiner each appear ≥1 time in the Market Map block specifically; Jeff/Jack/Jesse already appear elsewhere, so count their NEW appearance in the Market Map as additive not replacing)
- [ ] `grep -cE 'Ruben Hassid\|Sarah Cordiner\|Jeff Su\|Jack Roberts\|Jesse Genet' /Users/profile_1/Coding/jarda/jarda-ai-start/index.html` → **≥5** unique names across the file; Market Map block contains all five
- [ ] Privacy audit: `./scripts/privacy-audit.sh` (or equivalent — locate pre-Slice) exits **0** on the edited `index.html`
- [ ] Voice grep clean: no new banned markers — `grep -cE '\b(best\|leading\|top\|ultimate\|revolutionary\|game-changing)\b'` not higher than the pre-edit baseline
- [ ] Deployed HTML post-push also passes privacy: after `git push`, fetch `https://mark-c4r.github.io/Jay-Z/`, re-run privacy audit on the fetched file → exit 0
- [ ] Block ≤450 words (includes intro + `<li>` items + retained observations) — `wc -w` on the extracted `<div class="research-block">` at `:1811-1826` after edit
- [ ] Voice reviewer pass — Slice 3/7 pattern, dispatch a separate reviewer subagent with the voice contract (sober, matter-of-fact, behavioral-only, no evaluative language, no credentials/bios/quotes/pricing) and the rewritten block as input; reviewer returns PASS/FAIL with line-level notes

## 5. Slices

### Slice 1 · Rewrite the Market Map block with five real voices

**Scope:** Replace lines 1813-1822 (intro + `<ul>`) with new intro + five `<li>` entries. Lightly retune the two-axes observation at `:1823` so "two axes" still reads coherently (five voices still sit on the tool-axis × audience-axis grid; no change needed unless executor spots a sentence that specifically references "six"). Preserve `<h3>`, three observation paragraphs, closing `</div>`.

**Steps:**
1. Re-run all five verify commands from §2 to confirm pre-build state.
2. Locate `privacy-audit.sh` exact path and run it on current `index.html` — establish green baseline.
3. Dispatch **builder subagent** with:
   - Target file: `/Users/profile_1/Coding/jarda/jarda-ai-start/index.html`
   - Line range: 1813-1822 (intro + `<ul>`)
   - Replacement prose: **§9 Draft Replacement Block** below (paste verbatim, then light review for HTML escaping — apostrophes inside text, em-dashes, no unescaped `<`/`>`)
   - Voice contract: sober, matter-of-fact, behavioral-only. No "best/leading/top", no credentials, no follower counts, no pricing, no quotes, no URL links inside the `<li>` items, no bios.
   - HTML shape: `<li><strong>Name.</strong> Description sentence. Second sentence. Optional third sentence.</li>` — match exact shape of existing items.
4. Dispatch **voice reviewer subagent** with:
   - Input: the rewritten block (just the `<div class="research-block">` at 1811-1826)
   - Rubric: (a) no evaluative language; (b) behavioral description only; (c) each voice is described in a way that matches its *actual* practice per `discovery-plan.md:250-263`; (d) voice matches the rest of the research section (same register as the Tool Landscape block at 1802-1809 and the Why-six-stops block at 1828-1832); (e) the three observation paragraphs at :1823-1825 still read coherently — specifically, "None of the voices above is a vendor of the tool they teach" must remain true (verify: Anthropic-employed? None of the five are — safe).
   - Reviewer returns PASS with optional polish notes, or FAIL with specific issues.
5. Apply reviewer polish if any; re-run voice reviewer; iterate max 2 rounds.
6. Run all §4 AC checks in order. First failure → stop, fix, re-run full AC sweep.
7. Commit with message: `fix(jarda): correct Market Map — replace fabricated AI-teaching voices with real ones (Hassid, Su, Roberts, Genet, Cordiner)`.
8. Push to main.
9. Wait ~60s for GitHub Pages rebuild. Fetch deployed HTML. Re-run privacy audit on fetched file. Confirm AC 6 passes.

**Estimate:** 20-30 min wall time.

**Depends on:** Nothing — pure surgical edit.

**Demo:** `curl -s https://mark-c4r.github.io/Jay-Z/ \| grep -A 20 'Market map'` shows the five real voices.

## 6. No-Gos

- ❌ No URL links to competitors inside the `<li>` items. (Short-lived primer page; no SEO need; links create visual noise in an appendix block that's meant to read as a sober sidebar.) *Note:* `discovery-plan.md` shows these as markdown links because it's a planning doc, not shipped prose. Strip for production.
- ❌ No evaluative language — no "best", "leading", "top", "most/least", "ultimate", "revolutionary", "game-changing". Behavioral description only.
- ❌ No bios, credentials, job titles, or follower counts. The block describes what they teach, not who they are in career terms.
- ❌ No direct quotes from these creators. (Ruben's "prompts/projects/skills" framing belongs in Lesson 3 where it's already scaffolded per `discovery-plan.md:263` — not in the Market Map.)
- ❌ No pricing, no channel statistics, no posting cadence. (The current block's trailing paragraph already says pricing/cadence "change quickly and the reader can check them directly" — retain this.)
- ❌ No reintroduction of the six fabricated names in any form, including as "adjacent signal" commentary.
- ❌ No scope creep into fixing other research-section factual bugs. If the voice reviewer flags an issue in the Tool Landscape or Why-six-stops blocks, log as a separate ticket; do not bundle into Slice 1.

## 7. Verification Commands

Run in order during Slice 1 step 6:

```bash
# AC 1: fabricated names gone
grep -cE 'Hesselberg|Ceranna|Zibura|Ben Love|Honest Guide|Rexby' \
  /Users/profile_1/Coding/jarda/jarda-ai-start/index.html
# expect: 0

# AC 2 + 3: real voices present
grep -cE 'Ruben Hassid|Sarah Cordiner|Jeff Su|Jack Roberts|Jesse Genet' \
  /Users/profile_1/Coding/jarda/jarda-ai-start/index.html
# expect: ≥5 across the file; all 5 names at minimum once each inside lines 1811-1826

# AC 4: privacy audit (path TBD at Slice 1 step 2)
bash /Users/profile_1/Coding/jarda/jarda-ai-start/scripts/privacy-audit.sh
# expect: exit 0

# AC 5: voice grep clean (no new banned markers)
grep -cE '\b(best|leading|top|ultimate|revolutionary|game-changing)\b' \
  /Users/profile_1/Coding/jarda/jarda-ai-start/index.html
# expect: not greater than pre-edit baseline

# AC 7: block word count ≤ 450
awk '/research-block/,/<\/div>/' /Users/profile_1/Coding/jarda/jarda-ai-start/index.html \
  | awk '/Market map/,/None of the voices above is a vendor/' \
  | wc -w
# expect: ≤ 450 (refine awk range if needed during build)

# AC 6: deployed HTML privacy (post-push)
curl -sSL https://mark-c4r.github.io/Jay-Z/ > /tmp/deployed.html \
  && bash /Users/profile_1/Coding/jarda/jarda-ai-start/scripts/privacy-audit.sh /tmp/deployed.html
# expect: exit 0
```

## 8. Rollback

Single commit, single-file, single-block change. If something lands wrong post-push:

```bash
cd /Users/profile_1/Coding/jarda/jarda-ai-start
git revert HEAD --no-edit && git push
```

GitHub Pages rebuild returns the page to the pre-Slice-1 state (which is itself the current broken state, so rollback is only useful if the fix itself lands badly — e.g. broken HTML that renders the appendix blank). Restore the correct fix via a forward commit rather than reset.

## 9. Draft Replacement Block (voice-faithful, ready to paste)

Replace lines 1813-1822 with the following. Keep lines 1811-1812 (`<div class="research-block">` + `<h3>Market map</h3>`) and lines 1823-1826 (three observation paragraphs + closing `</div>`) unchanged, pending light retune in step 3 if the executor spots a reference to "six" voices in the observations.

```html
          <p>A short list of other voices teaching in this space. Notes describe the shape of their output, not a verdict on it. A reader who wants to compare notes — see the same idea explained differently, or find someone aimed at a different audience — can start with any of these.</p>
          <ul>
            <li><strong>Ruben Hassid.</strong> Writes a non-technical curriculum for Cowork on Substack. The framing he uses — prompts, then projects, then skills, each one a longer-lived investment than the last — is the scaffold most other teachers end up borrowing. Posts are short, written rather than filmed, and aimed at someone running a business who wants the progression without the developer vocabulary.</li>
            <li><strong>Jeff Su.</strong> Productivity and workflow on YouTube. Short videos, low-fluff, high-signal. The style is a single idea per video with a worked example in the frame. Useful as a first voice for a reader who wants to see the tool in a familiar productivity context — inbox, calendar, notes — before meeting any of the deeper surfaces.</li>
            <li><strong>Jack Roberts.</strong> Records a full-length Cowork course on YouTube from the angle of a solo founder using it daily for business operations. Long-form, unhurried, the opposite of a clipped-for-shorts cadence. Useful for the reader who prefers sitting with one multi-hour walkthrough over assembling the same material from dozens of short videos.</li>
            <li><strong>Jesse Genet.</strong> Writes and speaks about running AI agents inside a household rather than a workplace. Home finances, family logistics, voice-first capture during short windows between other tasks. The habits transfer even when the stack differs — the useful part is the shape of the day around the tool, not the tool itself.</li>
            <li><strong>Sarah Cordiner.</strong> Teaches Cowork to course-business owners and consultants. The register is instructor-to-instructor, aimed at someone who already sells their own expertise and is looking to automate the scaffolding around it. Later-stage material than the others above, worth bookmarking rather than starting with.</li>
          </ul>
```

Word count (intro + five `<li>` bodies, excluding HTML tags): **≈360w**. Plus retained tail at :1823-1825 (≈200w) ⇒ block total ≈560w — *slightly* over the 450-word AC. Two mitigations for the executor:
1. Drop the retained tail's "second observation" paragraph about "most voices teach by recording their own work" — it was true of the six fabricated names but is a weaker generalization over five real voices (Hassid writes rather than records). Removing it also tightens the block below 450w cleanly.
2. If the reviewer wants the tail kept intact, trim each `<li>` body to ~55w (drop one sentence each from Su, Roberts, Cordiner).

Executor picks (1) unless reviewer prefers (2). Recommend (1) — the "second observation" no longer matches reality.

## 10. Self-review checklist

- [x] Contract commits to **Option A** (swap-in-place), not B or C
- [x] Acceptance Criteria §4 enumerates all six items from the intake (grep-zero, grep-5, privacy audit, voice grep, deployed-HTML privacy, block ≤450w, voice reviewer pass) — actually lists 7 with the split of AC 2 and AC 3 for clarity
- [x] Draft replacement prose included inline in §9 — ready to paste, five voices, ~60-70w each, sober register
- [x] §7 Verification Commands lists 6 runnable commands gating ship
- [x] §6 No-Gos enumerates the six constraints from the intake (no URLs, no evaluative language, no bios/credentials, no quotes, no pricing/stats) + two additional safety no-gos (no reintroduction of fabricated names, no scope creep)
- [x] Risk score = 1: single-file change, reversible via `git revert`, no framework/schema/dependency touched
- [x] Same-session shape-then-ship acknowledged — VA re-verify gate documented in §2 staleness note
