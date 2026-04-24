---
ticket: jarda#reshape-2026-04-23 (Phase E — Slices 6 + 7)
status: active
project: jarda-ai-start
updated: 2026-04-24
parent: docs/plans/2026-04-23-jarda-reshape-refresher-primer.md
supersedes: docs/plans/2026-04-24-phase-d-slices-5-7-handoff.md
---

# Phase E Handoff — Slices 6 + 7

Fresh-session handoff. Slice 5 (4 research pages + dossier CSS) shipped in the previous session as 6 commits. Self-contained — new session should NOT need to re-read Slice 5's blueprint unless changing a Slice 5 decision.

## State at handoff (local commits, not pushed)

Ahead of `origin/main` by 12 commits total. Slice 5's 6 commits from this session:

| Commit | Slice | Content |
|--------|-------|---------|
| `d1ac4c4` | Slice 5 shape | PRD contract (392 lines, through 2 Codex review rounds) |
| `a36c22a` | Slice 5 shape | PRD preflight fixes (paths + Verified At + gate_override) |
| `c633477` | Slice 5.1 | Dossier CSS append to shared.css (+138 lines, 38 scoped selectors) |
| `dcfc927` | Slice 5.2 | market-clusters.html (5 peers × 4 blocks; + .gitignore refinement) |
| `c143cd2` | Slice 5.3 | ten-year-picture.html (4 archetypes + Zizka template) |
| `b1bf648` | Slice 5.4 | seo-and-discovery.html (AEO + 8 recipes + citations) |
| `db5c260` | Slice 5.5 | growth-opportunities.html (3-anchor frame: lane / revenue / gaps) |
| `8cc36a8` | Slice 5 close | PRD marked completed + AC boxes checked |

Plus 6 pre-existing commits from the earlier session (Slice 2–4). Final verification suite: 15/15 PASS.

**NOT shipped (this handoff's scope):**
- Slice 6 — proofread pass (voice + narrow-PII sweep)
- Slice 7 — ship (push to `origin/main` + GitHub Pages verify + Jay Z handoff)

## Critical privacy policy (read before any edit)

**Clarified by user in chat 2026-04-24 — this supersedes the earlier Phase D handoff's stricter policy.**

| Category | Policy |
|----------|--------|
| First name "Jarda" | **Fine to include.** Not PII-sensitive. |
| Email / phone / addresses | Excluded. |
| Wife / kids names | Excluded. |
| Referral codes | Excluded. |
| ICO numbers, s.r.o. / a.s. / spol. s r.o. / LLC / Ltd / Inc legal identifiers | Excluded. |
| Public brand names (`korunaevropy.cz`, `thebestviewpoints.com`) | Fine. |
| Public source URLs (Nightwatch, Frase, peer websites) | Fine. |

**Rule:** when two policy sources disagree, the later-timestamp statement wins. The in-chat clarification (2026-04-24) is authoritative. [README.md:5-7](README.md:5) still uses the stricter pre-clarification wording and is **a known follow-up** (Slice 6 §1 below).

**No solicitation on public research pages** — user rejected "WhatsApp" / "ping me" / "reach out" invites in `research/*.html`. The main page keeps its personal-letter closer at [index.html:247](index.html:247). Research pages keep only `.research-sources` citation lists in `.research-footer`.

## Slice 6 — Proofread pass

**Appetite.** S (30–60 min, possibly less given tight Slice 5 build).

**Inputs:**
- [voice-audit.md](docs/research/2026-04-24-reshape-research/voice-audit.md) — voice anchors + "doesn't sound like" hit-list.
- [index.html](index.html) (Slice 4 output) + all 4 `research/*.html` pages.
- [README.md](README.md) — privacy-policy wording needs softening.

**Checklist (updated for narrow-PII policy):**

1. **PII sweep (blocking):** Run the Slice 5 verification regex across all tracked public HTML:
   ```bash
   ! rg -ni '(@[a-z0-9][a-z0-9.-]*\.[a-z]{2,}|\+\d{2,3}[ -]?\d{3,}|I[ČC]O[ :]*\d{5,}|\bs\.r\.o\.|\ba\.s\.\b|\bspol\. s r\.o\.|\bLLC\b|\bLtd\b|\bInc\b)' index.html research/ styles/shared.css
   ```
   Zero matches required. Plus visual re-read of each page for non-pattern-matchable PII: wife/kids names, street addresses, referral codes.
2. **"Jarda" is no longer a block** — don't strip references to the first name. Per the 2026-04-24 policy clarification.
3. **Red-flag voice grep (blocking):** `! rg -n '\b(opinionated|convention|as we say|turns out|the truth is|in our view)\b' index.html research/` — zero matches.
4. **No-solicitation grep on research pages (blocking):** `! rg -qi 'whatsapp|ping me|reach out|dm me|message me|drop me a line' research/*.html`. The main page's personal-letter closer is fine.
5. **DHH-performed counter-sample sweep:** read every draft passage aloud. Flag anything that sounds like "Specificity beats breadth" / "Trust compounds slowly" / "clever prompting ages out" — absorb into "doesn't sound like" or rewrite.
6. **§1 opening drift check:** 4-paragraph opening should still name 5 peer names inline before any video facade. Verify peer_pos < facade_pos in [index.html](index.html).
7. **§4.2 thesis anchoring check:** verify §4.2 still names ≥2 peer-cluster names from §4.1 as evidence (currently Ceranna + Paul Zizka).
8. **§4.3 actionability check:** verify the first move is concrete enough that the reader could start it on Monday (not abstract advice).
9. **§4.4 humility clause B:** verify the WhatsApp anchor still appears at the END of §4.4 (last paragraph) — main page only.
10. **Video-companion copy check:** all 4 summaries start with "Hi Jay Z," and end with "—M" signoff.
11. **Jesse-asked-me decision:** [index.html:31](index.html:31) (§1 opening) reads "Jesse asked me to map out..." — leftover from D5. For the Jay Z placeholder version, "Jesse" is coincidentally the name of one of the video creators. Decide: keep (voice-natural) or rewrite.
12. **Copy length audit:** §4.1 ≈250w, §4.2 ≈200w, §4.3 ≈250w, §4.4 ≈150w per D8 budgets.
13. **README.md privacy-policy wording refresh:** [README.md:5-7](README.md:5) currently says *"The real name, real URLs, and real referral codes never land here. The page uses 'Jay Z' as the reader persona."* Soften to reflect the 2026-04-24 clarification — real URLs + referral codes still excluded; first name is fine. Candidate edit:
    > "This repo is a placeholder layout. Real URLs, referral codes, and personal contact info don't land here — the research-dossier pages reference the reader by first name for voice but scrub any PII (email/phone/address/family-member names/business registrations)."
14. **§6 pointer label (optional):** [index.html:240](index.html:240) says "Growth opportunities — Ceranna-shaped segment moves". Slice 5.5 delivers Ceranna as one of three anchors. If that reads as a broken promise, soften to "Growth opportunities — lane focus, revenue mix, reader-specific moves". Judgment call.

**Known issues to address:**
- `<style` inside any JS block: `rg -n '<style' index.html` — should only match strings inside code blocks, if at all.
- All research pages' `href="../styles/shared.css"` already verified with Slice 5's verification suite (15/15).

## Slice 7 — Ship

**Appetite.** S (30 min).

**Checklist:**

1. **Privacy pre-flight (blocking):**
   ```bash
   ! rg -ni '(@[a-z0-9][a-z0-9.-]*\.[a-z]{2,}|\+\d{2,3}[ -]?\d{3,}|I[ČC]O[ :]*\d{5,}|\bs\.r\.o\.|\ba\.s\.\b|\bspol\. s r\.o\.|\bLLC\b|\bLtd\b|\bInc\b)' $(git ls-files '*.html')
   ```
   Must exit 0 across all tracked HTML.
2. **Review git log since origin/main:** `git log origin/main..HEAD --oneline` — verify all 12+ commits are clean and intended (no accidental files, no leaked PII).
3. **Mark-readable check:** open `index.html` + all 4 `research/*.html` pages locally in a browser; click every facade; click every §6 pointer; click back-links; click citation links.
4. **Push to origin/main:** `git push origin main`. 12 commits will go up together (Phase C + D + E handoffs + Slice 2–5 builds + PRDs).
5. **GitHub Pages rebuild wait:** ~60–90s.
6. **Live verification:**
   ```bash
   curl -sSL https://mark-c4r.github.io/Jay-Z/ > /tmp/live.html
   # Privacy re-check on live HTML:
   ! rg -ni '(@[a-z0-9][a-z0-9.-]*\.[a-z]{2,}|\+\d{2,3}[ -]?\d{3,}|I[ČC]O[ :]*\d{5,}|\bs\.r\.o\.|\ba\.s\.\b|\bspol\. s r\.o\.|\bLLC\b|\bLtd\b|\bInc\b)' /tmp/live.html
   # Also fetch each research page to verify they're served:
   for p in market-clusters ten-year-picture seo-and-discovery growth-opportunities; do
     curl -sSL "https://mark-c4r.github.io/Jay-Z/research/$p.html" > "/tmp/live-$p.html"
     test -s "/tmp/live-$p.html" || echo "FAIL: $p not served"
   done
   ```
7. **Jay Z handoff:** Mark DMs the reader the URL. If he wants a real-name version, that's a separate operation (not from this repo).

**IMPORTANT:** `git init` is already done in `jarda-ai-start/`; remote `origin` is configured. Skip any `git init` step.

## Known issues / follow-ups (NOT blocking Slices 6–7)

1. **slice-2-blueprint.md D11 additive rows** — Slice 5 extended D11 wireframe B with 3 additive elements (noindex meta, preconnect pair, `.research-sources` footer). The blueprint wasn't updated. Small follow-up (~5 lines) when Slice 6/7 touches the blueprint anyway.

2. **Slice 4 gate_override reason** — [slice-4-main-page-build.md](docs/plans/prds/2026-04-24-reshape/slice-4-main-page-build.md) and [slice-5-research-pages-build.md](docs/plans/prds/2026-04-24-reshape/slice-5-research-pages-build.md) both use `gate_override: auto` for novel-path on `styles/`. After Slice 7 push lands, `styles/` will have origin/main commits within 60 days → novel-path check stops firing automatically. No cleanup needed; just note for future reference.

3. **Preflight script subtleties (documented in LEARNED 2026-04-24):**
   - CWD resolution: preflight runs from project root (per `project:` frontmatter); Source column paths must be submodule-relative.
   - Same-day shape-then-ship staleness: use per-row `Verified At` with hour-precision timestamps (e.g. `2026-04-24T05:50:00-0500`).
   - `Verify` cell parser rejects surrounding backticks (`D-VERIFY-BACKTICK`) and pipes (`D-VERIFY-PIPE`). Use plain shell commands or `test -s`, not table-delimiter-conflicting patterns.
   - Umbrella paths (`../docs/plans/archive/...`) may be rejected by preflight; move to `Evidence` column (prose) when file is outside submodule scope.

4. **Verification script bash gotcha (documented in LEARNED 2026-04-24):** `if rg pattern ... | head -5; then ...` checks `head`'s exit, NOT `rg`'s. For pattern-absence checks, use `! rg pattern ... && echo PASS || echo FAIL` (direct exit) rather than piping through `head`. Otherwise you get false-positive FAILs on patterns that don't match.

5. **`.gitignore` research/ exception** — Slice 5 converted `research/` from blanket-ignored to HTML-only-allowed. If future work adds non-HTML files in research/ (e.g., `.json` fixtures), they're auto-ignored. Targeted subpatterns already defined: `research/*.md`, `research/*.json`, `research/*.txt`, `research/private/`, `research/draft/`.

## Governance — do not re-litigate

- **Voice anchor:** "Mark writing to one friend over WhatsApp" — strip DHH/37signals cadence. Hi-Jay-Z / you / —M.
- **Red-flag denylist:** `opinionated|convention|as we say|turns out|the truth is|in our view` — zero matches in drafted copy.
- **Research-page footer convention:** `.research-sources` citation list only. NO WhatsApp / "ping me" / "reach out" solicitation on public research pages. Main page keeps its personal-letter closer.
- **Privacy policy (2026-04-24):** Narrow PII only — email/phone/address/family-names/legal-identifiers. First name "Jarda" is fine.
- **70/30 video consumption split:** learning videos (Jeff Su, Jack Roberts) = ~150w memory-trigger. Interview videos (Jesse × 2) = ~290–295w stand-alone + 2–3 load-bearing quotes.
- **Same-session-ship VA pattern:** rewrite VA rows to post-build state per LEARNED 2026-04-19. Use hour-precision `Verified At` timestamps.
- **Force-track PRDs only, not backlog:** `git add -f docs/plans/prds/…` for each PRD individually. Never `git add docs/` bulk.
- **Per-slice-PRD pivot:** each slice gets its own `/shaping` cycle. Risk score governs depth. Slice 6 + 7 are S; no Codex review needed.

## Critical file paths (quick reference)

- **This handoff:** [docs/plans/2026-04-24-phase-e-slices-6-7-handoff.md](docs/plans/2026-04-24-phase-e-slices-6-7-handoff.md)
- **Slice 5 PRD (authoritative for dossier conventions):** [docs/plans/prds/2026-04-24-reshape/slice-5-research-pages-build.md](docs/plans/prds/2026-04-24-reshape/slice-5-research-pages-build.md)
- **Slice 2 blueprint (D11/D12 baseline):** [docs/plans/prds/2026-04-24-reshape/slice-2-blueprint.md](docs/plans/prds/2026-04-24-reshape/slice-2-blueprint.md)
- **Umbrella reshape plan:** [docs/plans/2026-04-23-jarda-reshape-refresher-primer.md](docs/plans/2026-04-23-jarda-reshape-refresher-primer.md)
- **Research vault:** [docs/research/2026-04-24-reshape-research/](docs/research/2026-04-24-reshape-research/) + [docs/research/2026-04-21-round-2-research/](docs/research/2026-04-21-round-2-research/)
- **Memory anchors (user-scope):** `~/.claude/projects/-Users-profile-1-Coding-jarda/memory/` — voice-anchor + video-consumption-split + reshape-memories

## First action in the new session

1. Read this handoff end-to-end.
2. Run the Slice 5 verification suite to confirm nothing has drifted:
   ```bash
   cd /Users/profile_1/Coding/jarda/jarda-ai-start
   bash -c 'for p in market-clusters ten-year-picture seo-and-discovery growth-opportunities; do test -s "research/$p.html" || echo "MISSING: $p"; done'
   ```
3. Invoke `/shaping` on Slice 6 (`--no-research`; context is all here). Expect risk 1–2, appetite S. Skip Codex review (policy: optional at risk ≤ 3 + reversible + single project).
4. Build Slice 6 proofread changes (likely README edit + minor copy polish).
5. Move directly to Slice 7 ship.

**HARD PRIVACY GUARD before every commit:**
```bash
! rg -ni '(@[a-z0-9][a-z0-9.-]*\.[a-z]{2,}|\+\d{2,3}[ -]?\d{3,}|I[ČC]O[ :]*\d{5,}|\bs\.r\.o\.|\ba\.s\.\b|\bspol\. s r\.o\.|\bLLC\b|\bLtd\b|\bInc\b)' $(git ls-files '*.html')
```
Must exit 0.
