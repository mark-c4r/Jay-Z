# Round-2 PRD Pipeline — INDEX

Authored: 2026-04-22 · pre-state commit: `f1cb7b9` (Day-2 ship)
Goal: 20 atomic PRDs + per-PRD Codex R2 + handoff — ready for Sonnet execution, one PRD per session.

## Status legend

- `draft` — written by Opus; Codex review pending
- `codex-reviewing` — dispatched to Codex R2
- `codex-p0-fix-pending` — Codex returned findings; Opus folding P0s
- `approved` — P0s folded, ready for Sonnet pickup
- `in-progress` — a Sonnet session has claimed this PRD
- `completed` — shipped via `/ship`; next PRD in dep chain unlocked

## PRD table

| PRD | Title | Appetite | Risk | Status | Depends on | Unblocks | Codex verdict (R1) | P0/P1 |
|---|---|---|---|---|---|---|---|---|
| [C3.1](C3/C3.1-prereq-card.md) | Prereq/identity card (markup + CSS + 6 slots) | M | 5 | completed | — | C3.2, C7.2 | REJECT | 3/3 |
| [C3.2](C3/C3.2-runner-framing.md) | Runner-framing consolidation | S-M | 3 | completed | C3.1 | C3.4 | REJECT | 3/4 |
| [C3.3](C3/C3.3-11gb-cure.md) | Stop 4 11GB cure | S | 3 | completed | — | C2.3, C3.4 | REJECT | 3/3 |
| [C3.4](C3/C3.4-verify-pass.md) | C3 verification pass | S | 1 | completed | C3.1, C3.2, C3.3 | — | REJECT | 3/4 |
| [C7.2](C7-structural/C7.2-ack-sentence.md) | Customization-acknowledgment 7th slot | S | 2 | completed | C3.1 | — | REJECT | 3/3 |
| [C7.3](C7-structural/C7.3-block-stubs.md) | Empty block stubs D/E/F/G | S | 2 | completed | — | C7.4, C7.5, C7.7, C7.8 | REJECT | 2/1 |
| [C5.1](C5/C5.1-normalize-jsons.md) | Normalize chapter JSONs + videoChapters | M | 4 | completed | — | C5.3, C5.4 | REJECT | 1/3 |
| [C5.2](C5/C5.2-activate-facade.md) | Extend activateFacade signature | S | 3 | completed | — | C5.3, C5.4, C2.2 | REJECT | 2/3 |
| [C5.3](C5/C5.3-render-chapters.md) | Render chapter lists per facade | M | 3 | completed | C5.1, C5.2 | C5.4, C5.5 | REJECT | 1/4 |
| [C5.4](C5/C5.4-click-handlers.md) | Chapter click handlers | M | 4 | completed | C5.1, C5.2, C5.3 | C5.5 | REJECT | 3/2 |
| [C5.5](C5/C5.5-a11y-keyboard.md) | C5 a11y + keyboard verification | S | 1 | approved | C5.1, C5.2, C5.3, C5.4 | — | REJECT | 3/2 |
| [C2.1](C2/C2.1-scroll-sync.md) | Topbar scroll-sync IO + fallback | M | 4 | completed | — | — | REJECT | 5/3 |
| [C2.2](C2/C2.2-touch-click-guard.md) | Facade touchend handler | M | 4 | completed | C5.2 | — | REJECT | 2/2 |
| [C2.3](C2/C2.3-stuck-stop4.md) | Stop 4 "Stuck?" cure | S | 2 | completed | C3.3 | — | REJECT | 4/3 |
| [C2.4](C2/C2.4-stuck-footer.md) | Footer fallback | S | 2 | completed | — | — | REJECT | 3/2 |
| [C7.4](C7-content/C7.4-block-D-market.md) | Block D market clusters | M-L | 5 | approved | C7.3 | — | REJECT | 3/3 |
| [C7.5](C7-content/C7.5-block-E-growth.md) | Block E growth opportunities | M | 4 | approved | C7.3 | C7.6 | REJECT | 2/2 |
| [C7.6](C7-content/C7.6-block-F-plus-bridge.md) | Block F+ bridge | S | 2 | approved | C7.5 | — | REJECT | 3/2 |
| [C7.7](C7-content/C7.7-block-F-seo.md) | Block F SEO recipes | M | 3 | approved | C7.3, C7.6 | — | REJECT | 3/3 |
| [C7.8](C7-content/C7.8-block-G-10year.md) | Block G 10-year picture | M | 5 | approved | C7.3 | — | REJECT | 4/3 |

**Totals:** 20 PRDs · 20 Codex-R1 reviewed (2026-04-22) · 56 P0s + 55 P1s total · **Phase E folding complete; remaining work is Sonnet execution of the approved PRDs.**

## Status legend (updated)

- `draft` — written by Opus; Codex review pending
- `codex-p0-fix-pending` — Codex reviewed; P0s identified; historical intermediate state before Phase E folding
- `approved` — P0s folded + R2-verify (optional); ready for Sonnet pickup
- `in-progress` — a Sonnet session has claimed this PRD
- `completed` — shipped via `/ship`; PRD's own `status:` field flipped to `completed` post-ship

## Codex review summary

All 20 reviews saved as `<prd-id>.codex-r2.md` siblings to each PRD. Common P0 patterns (folder should address preemptively with a single fix pass before per-PRD folding):

1. **Missing "mark status: completed" step** — already fixed at INDEX + TEMPLATE level; individual PRDs inherit the step from TEMPLATE's "Post-ship: mark PRD completed (MANDATORY)" section. Some per-PRD reviews still flag the absence in the PRD body — those notes can be marked resolved.
2. **VA commands using `\|` regex alternation** — fixed in 4 PRDs (C3.1 ×2, C5.3, C7.2) preemptively. Any remaining per-PRD instances flagged by Codex should use `rg -c -e 'pat1' -e 'pat2'` form.
3. **AC scoping too broad** — many ACs verify whole-file when stable block IDs exist. Fold pattern: wrap each AC's command in `sed -n '/id="<block-id>"/,/id="<next-block-id>"/p index.html | rg -c ...`.
4. **Edit anchor uniqueness** — some anchors aren't unique in the current source. Fold pattern: grep-count the anchor text during fold; if >1 match, extend the anchor with disambiguating context.
5. **Copy locks missing verbatim ACs** — some Verify commands check for partial strings instead of full copy-lock sentences. Fold pattern: turn each Copy lock into an explicit `rg -c "<full sentence>"` AC.

## Dependency graph (execution order)

```
Tier 0 (no unshipped deps):   C3.1 ─┐   C3.3 ─┐   C5.1 ─┐   C5.2 ─┐   C2.1   C2.4   C7.3 ─┐
                                    │         │         │         │                        │
Tier 1 (first-level):         C3.2 ─┤  C2.3 ─┤  C5.3 ─┤   C2.2    C7.2 (needs C3.1)        C7.4, C7.5, C7.8 (need C7.3)
                                    │         │         │
Tier 2 (second-level):        C3.4 ─┤         │  C5.4 ─┤                          C7.6 (needs C7.5)
                                              │         │
Tier 3 (third-level):                         │  C5.5 ─┤                          C7.7 (needs C7.3 + C7.6)
                                                        │

```

Simpler ordering for Sonnet:

1. **Tier 0 (parallelizable, no deps):** C3.1, C3.3, C5.1, C5.2, C2.1, C2.4, C7.3
2. **Tier 1:** C3.2, C2.3, C5.3, C2.2, C7.2, C7.4, C7.5, C7.8
3. **Tier 2:** C3.4, C5.4, C7.6
4. **Tier 3:** C5.5, C7.7

## Sonnet pickup protocol

Each Sonnet session, in order:

1. **Read this INDEX.md.** Find the lowest-numbered PRD with `status: approved` AND all `depends-on` entries `status: completed`.
2. **Open that PRD.** Run its "Sonnet pickup protocol" bash block verbatim. If any assertion fails, STOP — flag drift to operator, do not proceed.
3. **If green:** execute the Work/Edit sections verbatim. Grep-verify each AC as you go.
4. **Ship via `/ship`** with the PRD's commit template. Push to origin + monitor Pages deploy + smoke-check.
5. **Mark the PRD `status: completed` in its OWN frontmatter** (`sed -i.bak -e 's/^status: approved$/status: completed/' <prd-path>` then remove the `.bak`, commit this frontmatter change as a trailing chore commit OR include in the /ship commit). **This is load-bearing — downstream PRDs grep this file for `^status: completed` in their pickup protocol; a shipped-but-unmarked PRD strands every dependent PRD.**
6. **Update this INDEX:** flip the PRD row's `Status` column to `completed`. Update LEARNED.md if anything new emerged. Exit the session.

**Never skip** steps 5 or 6. **Never skip** the pickup protocol. **Never** edit a PRD whose `depends-on` isn't complete. **Never** fold two PRDs into one commit unless the commit template permits it.

## Cross-cluster contract map

| Contract | Producer | Consumer | Enforcement |
|---|---|---|---|
| Prereq-card 6-slot structure | C3.1 | C7.2 (appends 7th slot) | C7.2 pickup checks C3.1 `status: completed` |
| Stop 4 main-block anchor order | C3.3 (11GB cure replaces "Nothing is hidden") | C2.3 (appends "Stuck? Screenshot" at END) | C2.3 pickup checks C3.3 completed + re-greps anchor |
| `activateFacade` signature | C5.2 (`(facade, startOverride)`) | C2.2 (uses extended sig for idempotent guard) | C2.2 pickup checks C5.2 completed + re-greps signature |
| Appendix block IDs | C7.3 (stubs for D/E/F/G) | C7.4-C7.5-C7.8 and the F/F+ lane (C7.6 bridge, then C7.7 fill) | C7.x pickup checks C7.3 completed + re-greps id="research-…" |
| Footer existence decision | C2.4 (creates or uses `#completion-reveal`) | (terminal — no downstream consumer) | Documented inline in C2.4 PRD |

## Handoff doc

The new handover for Sonnet sessions is [`../../2026-04-22-HANDOFF-prd-pipeline.md`](../../2026-04-22-HANDOFF-prd-pipeline.md).
The prior Day-2 handover [`../../2026-04-22-HANDOFF-day2-round2-build.md`](../../2026-04-22-HANDOFF-day2-round2-build.md) is superseded.

## Codex review artifacts

Per-PRD Codex R2 reviews are saved as `<prd-id>.codex-r2.md` siblings to each PRD file. The dispatch + fold procedure is documented in [`CODEX-ORCHESTRATION.md`](CODEX-ORCHESTRATION.md).
