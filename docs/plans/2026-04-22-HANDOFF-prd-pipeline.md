---
ticket: jarda-ai-start#round2-prd-pipeline
status: active
appetite: L (multi-session — Phase E folding + Phase G Sonnet execution × 20)
project: jarda-ai-start
updated: 2026-04-22
supersedes: 2026-04-22-HANDOFF-day2-round2-build.md
files: [docs/plans/prds/2026-04-22-round-2/*]
---

# ROUND-2 PRD PIPELINE HANDOFF — Phase G execution

**For:** next Sonnet sessions (Phase G execution, one PRD per session).

**State at handoff:** 10 of the 20 indexed PRDs are completed, 6 are approved and Sonnet-ready now, and 4 are approved but still waiting on deps. `C0.1-deploy.md` is already completed as a separate operational PRD outside the 20-PRD count.

**You are NOT re-shaping anything.** Round-2 cluster decisions are locked at master-shape commit `897eb8b` + R2v folds. Each PRD's core design is settled; Codex flagged execution-readiness issues (memory-based VAs, AC scoping, anchor uniqueness, copy lock precision), not design issues.

---

## Historical note — Phase E folder prompt (archival only)

Phase E is complete. The block below is kept only as historical context; do not use it as the next-session prompt.

```
I'm picking up the round-2 PRD pipeline for Phase E (fold Codex P0s).

Do these in order:

1. Read docs/plans/2026-04-22-HANDOFF-prd-pipeline.md (this doc) in full.
2. Read docs/plans/prds/2026-04-22-round-2/INDEX.md — see the 20-PRD status + each verdict + P0/P1 counts.
3. cd /Users/profile_1/Coding/jarda/jarda-ai-start && git log --oneline -12 — confirm HEAD is b3512b2 or a descendant, and the 7 pipeline commits (57b4de2→b3512b2) are all present.
4. Pick ONE cluster to fold (C3 or C7-structural recommended for first session — smaller P0 surface + unblocks downstream). Read every PRD in the cluster + every .codex-r2.md sibling.
5. Fold P0s per PRD (see "Phase E folding procedure" in this doc). Update frontmatter status → approved + codex-verdict accordingly.
6. Optionally re-dispatch Codex R2 in verification mode for the folded PRD (round cap: 2 per PRD per shape-up.md).
7. Commit the folded cluster. Move on to next cluster or hand off.

When the cluster is status: approved, Sonnet can pick it up.
```

---

## Part 1 — State snapshot

### Pipeline commits (in order)

| SHA | Phase | What |
|---|---|---|
| `57b4de2` | A | Scaffold: dir + TEMPLATE + INDEX + CODEX-ORCHESTRATION |
| `23191dc` | B | Anthropic docs snapshot (C3.0-P0 gate) |
| `bbfe2f2` | C1 | C3 cluster — 4 PRDs |
| `621cdef` | C2 | C7-structural — 2 PRDs |
| `28ef2b8` | C3 | C5 cluster — 5 PRDs |
| `935a046` | C4 | C2 cluster — 4 PRDs |
| `fbab616` | C5 | C7-content — 5 PRDs |
| `2c9fb6d` | D | 20 Codex R2 reviews dispatched + saved |
| `b3512b2` | E prep | INDEX verdicts + 20 frontmatter flips → codex-p0-fix-pending |
| (this doc) | F | Handoff doc + supersede |

### Status across the 20 indexed PRDs (as of 2026-04-22)

10 PRDs are `completed`:
- C3.1, C3.2, C3.3, C3.4, C7.2, C7.3, C2.3, C2.4, C5.1, C5.2

6 PRDs are `approved` and Sonnet-ready now (all deps already complete):
- C2.1, C2.2, C5.3, C7.4, C7.5, C7.8

4 PRDs are `approved` but still waiting on deps:
- C5.4 (needs C5.3)
- C5.5 (needs C5.3 + C5.4)
- C7.6 (needs C7.5)
- C7.7 (needs C7.6)

`docs/plans/prds/2026-04-22-round-2/C0.1-deploy.md` is completed outside the 20-row INDEX, so the full planning-doc total is 11 completed items as of this handoff: 10 indexed PRDs + C0.1.

See INDEX.md for the canonical 20-PRD table and per-PRD depends-on fields.

### Anthropic-docs snapshot freshness

The C3.x PRDs depend on `ANTHROPIC-DOCS-SNAPSHOT.md` (access date 2026-04-22). Staleness trigger is **2026-05-06** — after that, re-run Phase B (WebFetch claude.com/pricing + support.claude.com/connectors) before folding C3 PRDs.

---

## Part 2 — Phase E folding procedure (Opus next session)

For each cluster (C3, C7-structural, C5, C2, C7-content), follow this loop:

### Step 1: Read the inputs

- `INDEX.md` for the cluster's row data (verdicts + P0 counts)
- Each PRD file in the cluster
- Each `<prd-id>.codex-r2.md` sibling — this is the source of truth for what to fold
- Cluster's source anchors in `index.html` — re-grep to confirm current state still matches

### Step 2: Fold P0s per PRD

For each PRD in the cluster, open the `.codex-r2.md` and work through P0s in order:

1. **Memory-based VA errors** — if Codex ran a VA verify command and got a mismatch, update the VA row's command to something that actually returns the expected result on current source. Common fixes:
   - Wrong line number in VA ref column → update to current line via `rg -n`
   - `\|` regex alternation → replace with `-e pattern1 -e pattern2` form
   - Expected-result mismatch → update expectation to actual (if the CLAIM is still correct) OR update command to match the actual current source
2. **Non-unique Edit anchors** — grep the anchor text; if >1 match, extend the anchor with surrounding disambiguator text (a few lines of context before/after).
3. **AC scoping (whole-file → block-local)** — wrap each AC's verify command in `sed -n '/id="<block>"/,/id="<next-block>"/p index.html | rg -c ...`. Pick the block's stable ID (all appendix blocks have ids per C7.3; stops have `id="stop-N"`; prereq-card scoped via `sed -n '/class="prereq-card"/,/<\/aside>/p'`).
4. **Copy-lock precision** — for every `> quoted copy block` in the PRD, ensure there's a matching AC with `rg -c "<full verbatim sentence>" index.html` → 1. If Codex flagged a partial-match AC, expand it.
5. **Cross-cluster contract drift** — if a downstream PRD's pickup-protocol grep doesn't exactly match what this PRD enforces, fix either this PRD's enforcement wording OR the downstream PRD's pickup check, depending on which is "more right."
6. **Pickup protocol fail-closure** — confirm `set -e` at the top, every `rg -c` + `grep -q` chained with `|| { echo DRIFT; exit 1; }`, and every `depends-on` has a `grep -q "^status: completed"` check.

### Step 3: Fold P1s (selectively)

P1s are friction-adds, not blockers. Fold if:
- Fix doesn't expand scope
- Fix doesn't require new decisions
- Fix tightens verification surface

Otherwise leave as `Known risks + mitigations` bullet in the PRD or call out explicitly in the commit body.

### Step 4: Update frontmatter

```yaml
status: approved            # was codex-p0-fix-pending
codex-verdict: APPROVE_WITH_REVISIONS   # never APPROVE without R2v; never lower than actual
```

Keep `codex-reviewed-at` as the R1 timestamp. If you re-run R2 in verification mode (see Step 5), append a `codex-r2v-at: <ISO>` field.

### Step 5 (optional): Re-run Codex in verification mode

Per `~/.claude/rules/shape-up.md` §Cross-Model Review round cap (2 per doc), if R1 flagged structural issues (not just cosmetic), dispatch Codex R2-verify:

```bash
# Example for C3.1:
codex exec --sandbox read-only --skip-git-repo-check --color never --json - \
  > /tmp/codex-r2v/C3.1.jsonl <<PROMPT
You are verifying a PRD that has been folded from Codex R1 findings.

PRD file: docs/plans/prds/2026-04-22-round-2/C3/C3.1-prereq-card.md
R1 review: docs/plans/prds/2026-04-22-round-2/C3/C3.1.codex-r2.md

Task: confirm every R1 P0 is addressed. Report:
  - Addressed: list of R1 P0 ids + how they were resolved
  - Still open: list of R1 P0 ids + why the fold didn't address them
  - New regressions: any issues introduced by the fold
  - Final verdict: APPROVE | APPROVE_WITH_REVISIONS | REJECT

Budget: ~1/3 the original review cost (focused verification, not full review).
PROMPT
```

Extract + append to `<prd>.codex-r2.md` under a `## Round 2 — verification` heading.

### Step 6: Commit the folded cluster

```bash
git add -f docs/plans/prds/2026-04-22-round-2/<cluster>/
git commit -m "shape(round-2-prds/<cluster>): Phase E fold — <N> PRDs approved

<summary of folds per PRD>

PRD: <cluster>
Codex-folded: R1 → <R1v-date if R2v ran>
"
```

---

## Part 3 — Sonnet dispatch protocol (current queue)

The remaining queue is now in execution mode. The one-off deploy gate (`C0.1-deploy.md`) is already complete, so Sonnet sessions can pick off the indexed PRDs directly in dependency order from INDEX.md.

### Sonnet session boot protocol

Start each Sonnet session with this prompt:

```
I'm executing one PRD from the round-2 pipeline. Pickup protocol:

1. Check docs/plans/prds/2026-04-22-round-2/C0.1-deploy.md.
   - C0.1 is status: completed (completed 2026-04-23). Skip directly to step 2.
2. Read docs/plans/prds/2026-04-22-round-2/INDEX.md.
3. Find the lowest-numbered PRD in the dependency graph where:
   - status: approved
   - all `depends-on` entries have status: completed
4. Open that PRD.
5. Run its "Sonnet pickup protocol" bash block VERBATIM. Must pass cleanly.
6. If any assertion fails → STOP. Flag to operator with the failing check.
7. If clean → execute the "Work — exact edits" sections verbatim.
8. Verify each AC as you go (run every verify command, confirm expected result).
9. Ship via `/ship <ticket>` — see PRD's commit template.
10. After ship success: update PRD frontmatter status → completed (TEMPLATE.md "Post-ship" section, or the PRD's local equivalent for C0.1).
11. If the PRD is in INDEX.md, update its row Status column → completed. Commit.
12. Exit the session.

Never skip the metadata update step. Downstream PRDs grep `status: completed` to unblock, and this handoff keeps the completed deploy-gate history explicit for later sessions.
```

### Sonnet context budget

A typical PRD is 150-400 lines. Plus:
- index.html (~2200 lines current, ~2800 post-build)
- The PRD's `.codex-r2.md` (~60 lines)
- Handoff doc (~400 lines — this file)
- Rules files (~800 lines across code-principles, shape-up, workflow)

Total ~4500 lines. Well within 200K Sonnet context. Room for iteration + logs.

### Order of Sonnet sessions (dependency-aware)

**Deploy gate (completed — do not re-run):**
- C0.1 — DONE. Pushed local `main` to origin, Pages reached `built`, live 4-marker smoke (`A primer by Mark` ×2, `11 GB`, `read-alongs`) + `noindex, nofollow` singleton all verified. Completed 2026-04-23.

**Ready now (all deps already complete; INDEX lowest-numbered rule applies within this set):**
- C2.1
- C2.2
- C5.3
- C7.4
- C7.5
- C7.8

**Waiting on deps (do not dispatch until the dependency listed is completed):**
- C5.4 waits on C5.3
- C5.5 waits on C5.3 + C5.4
- C7.6 waits on C7.5
- C7.7 waits on C7.6

If you are following the lowest-numbered-ready rule strictly, the first indexed PRD after C0.1 is C2.1.

### If Sonnet pickup fails (drift detected)

1. Sonnet reports the failing assertion back to operator.
2. Operator decides: (a) re-run Phase E to fix the PRD, (b) manually re-grep and patch, (c) skip and try a different PRD.
3. Do NOT let Sonnet build despite drift — the fail-closure is load-bearing.

---

## Part 4 — Cross-cluster contracts (unchanged from original handover)

These are still the truth. Sonnet pickups enforce them via `depends-on` checks:

1. **C3.1 → C7.2** — C7.2 appends 7th slot to C3.1's prereq-card.
2. **C3.3 → C2.3** — C2.3 appends "Stuck?" after C3.3's 11GB cure in Stop 4.
3. **C5.2 → C2.2** — C2.2 uses C5.2's 2-param signature + idempotent guard.
4. **C7.3 → C7.4/C7.5/C7.7/C7.8** — content PRDs fill C7.3's stubs.
5. **C7.5 → C7.6** — bridge paragraph goes after Block E.
6. **C2.4 footer choice** — resolved at PRD write time: create new `<footer>`.

---

## Part 5 — Privacy, voice, style invariants (unchanged)

Every PRD's pickup protocol and verify block checks:
- `rg -ci 'jarda|thebestviewpoints|korunaevropy|jardaphoto' index.html || echo 0` → 0
- `rg -ci 'guinness|45 peak|45 european|stockholm.*base' index.html || echo 0` → 0
- `rg -c 'name="robots"' index.html` → 1 (singleton noindex)
- `rg -c "Jay Z|Jay-Z" index.html` → ≥1 (placeholder preserved)
- `rg -c '<section id="stop-[0-9]"' index.html` → 6 (stop count preserved)
- Banned clichés: "You must", "Game-changing", "Revolutionary", "must-read", "definitive", "the best thing", "AI will change everything" → 0 each

---

## Part 6 — Environmental context

### Shell
- **zsh $status read-only** — never use `status=...` as a bash variable name (documented LEARNED entry, recurred once already during Day-2 ship). Use `build_status`, `deploy_state`, `rc`, etc.
- Pre-existing `.qa-reports/` directory from C4a ship — gitignored via umbrella's implicit handling; not a concern.

### Tools
- `codex exec` v0.117.0+ available at `/usr/local/bin/codex`
- `gh` CLI authenticated as `mark-c4r`
- `yt-dlp`, `python3`, `node` all available

### Deploy
- Public repo: `mark-c4r/Jay-Z` (currently at `f1cb7b9` live)
- Pages deploy: 30-60s from push
- Check: `gh api repos/mark-c4r/Jay-Z/pages/builds/latest --jq '.status'` — 'built' means done

---

## Part 7 — What this handover explicitly does NOT contain

- **No P0 fix content** — the `.codex-r2.md` files have the P0 details; this doc only documents the procedure.
- **No Sonnet-session prompt beyond the boot protocol** — each Sonnet session reads its PRD and builds; no additional scaffolding needed.
- **No re-shaping of cluster scope** — master shape `docs/plans/2026-04-21-round-2-master.md` remains authoritative.
- **No live-site edits** — Phase E + execution-sessions touch `index.html`; this handoff only covers the PRD pipeline meta-work.

---

## Part 8 — First commands for the next Opus (Phase E) session

```bash
cd /Users/profile_1/Coding/jarda/jarda-ai-start

# 1. Orientation
git log --oneline -12
git status
test "$(git rev-parse HEAD)" = "$(git rev-parse origin/main 2>/dev/null || git rev-parse HEAD)" && echo "in sync"

# 2. PRD status
ls docs/plans/prds/2026-04-22-round-2/
cat docs/plans/prds/2026-04-22-round-2/INDEX.md | head -60

# 3. Pick the cluster to fold (C3 has 4 PRDs, simplest start)
ls docs/plans/prds/2026-04-22-round-2/C3/
cat docs/plans/prds/2026-04-22-round-2/C3/C3.1.codex-r2.md  # start with the first PRD's review

# 4. Confirm source state
rg -n "<main id=\"main\"" index.html
rg -n "Nothing is hidden" index.html

# 5. Begin folding (see Part 2 Step 2 above)
```

---

*End of handover. Next Opus session: focus on ONE cluster per session; fold P0s; commit; hand off to next cluster or to Sonnet. Next Sonnet session: see Part 3.*
