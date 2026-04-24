---
ticket: jarda#reshape-2026-04-23 (Phase D — Slice 5)
status: active
appetite: M
risk_score: 3
project: jarda-ai-start
updated: 2026-04-24
parent: jarda-ai-start/docs/plans/2026-04-23-jarda-reshape-refresher-primer.md
handoff: jarda-ai-start/docs/plans/2026-04-24-phase-d-slices-5-7-handoff.md
files:
  - jarda-ai-start/styles/shared.css (append)
  - jarda-ai-start/research/market-clusters.html (new)
  - jarda-ai-start/research/ten-year-picture.html (new)
  - jarda-ai-start/research/seo-and-discovery.html (new)
  - jarda-ai-start/research/growth-opportunities.html (new)
---

# Slice 5 — Research pages build

## Context

Phase D of the reshape. Slices 2–4 shipped in the previous session: Slice 2 locked 12 decisions including the research-page wireframe (D11) + dossier aesthetic (D12); Slice 3 extracted inline CSS to `styles/shared.css`; Slice 4 rewrote `index.html` per wireframe A and committed `research/*.html` hrefs at [index.html:237-240](jarda-ai-start/index.html:237).

Those four hrefs are now dead links. This slice builds the target pages plus the dossier CSS (`.research-dossier`, `.observed`, `.inferred`, `.may-mean`, `.experiment`, `.research-header`, `.dossier-humility`, `.back-link`, `.research-footer`). Content is drafted from Phase C research already on disk — no new research.

**Privacy policy (clarified in chat 2026-04-24):** The first name "Jarda" is fine to include in public HTML — it's not PII-sensitive. What stays out: email addresses, phone numbers, home/business addresses, names of the reader's wife or kids, referral codes, and exact registered-business identifiers (ICO numbers, s.r.o. / a.s. / spol. s r.o. / LLC legal names). Those have no place in research-dossier content anyway. The earlier handoff's `! rg -q "Jarda"` hard-grep was belt-and-suspenders; the actual bar is narrower (PII only).

**Reader persona (Slice 2 D5, unchanged here):** Main page already uses "Jay Z" throughout as reader name ([index.html:9,27,30](jarda-ai-start/index.html:9)). Slice 5 pages continue the persona for voice consistency. The privacy clarification does NOT revoke the Jay-Z persona — persona is a voice choice (Slice 2 D5 decision); privacy is a PII-leak bar. They're orthogonal.

**Policy coherence flag (out of Slice 5 scope):** [README.md:5-7](jarda-ai-start/README.md:5) currently states "The real name, real URLs, and real referral codes never land here." That line is stricter than the 2026-04-24 clarification (real name OK; URLs / referral codes still excluded). Resolution rule: **when two policy sources disagree, the later-timestamp statement wins** — the in-chat clarification (2026-04-24) is the authoritative policy. README wording should be softened in a follow-up pass (Slice 6 candidate — see Follow-ups §1 below). Slice 5 does not edit README.

Slice 6 (proofread) and Slice 7 (ship) are separate, deferred to later sessions.

## Verified Assumptions

| Claim | Source | Status | Verify |
|-------|--------|--------|--------|
| index.html §6 has 4 research-page hrefs | [`jarda-ai-start/index.html:237-240`](jarda-ai-start/index.html:237) | VERIFIED | rg -n 'href="research/' jarda-ai-start/index.html |
| index.html §1 names 5 peers: Ceranna, Avvagraphy, 2 Brides, Honest Guide, Paul Zizka | [`jarda-ai-start/index.html:34`](jarda-ai-start/index.html:34) | VERIFIED | rg -n 'Ceranna, Avvagraphy, 2 Brides, Honest Guide, Paul Zizka' jarda-ai-start/index.html |
| §4.1 has 1-paragraph sketch per peer (the "full map") | [`jarda-ai-start/index.html:180-184`](jarda-ai-start/index.html:180) | VERIFIED | rg -c 'Ceranna Photography\|Avvagraphy\|2 Brides\|Honest Guide\|Paul Zizka' jarda-ai-start/index.html |
| shared.css is 1617 lines, ends at line 1616 (closing media query) | [`jarda-ai-start/styles/shared.css:1616`](jarda-ai-start/styles/shared.css:1616) | VERIFIED | wc -l jarda-ai-start/styles/shared.css |
| .research-block already exists (from pre-reshape) | [`jarda-ai-start/styles/shared.css:1246`](jarda-ai-start/styles/shared.css:1246) | VERIFIED | rg -n '^\.research-block' jarda-ai-start/styles/shared.css |
| .observed / .inferred / .may-mean / .experiment do NOT yet exist | n/a | VERIFIED | ! rg -q '^\.(observed\|inferred\|may-mean\|experiment)\\b' jarda-ai-start/styles/shared.css |
| research/ directory does not exist yet | n/a | VERIFIED | ! test -d jarda-ai-start/research |
| Fonts loaded via `<link>` in index.html head (Fraunces + Inter) | [`jarda-ai-start/index.html:12`](jarda-ai-start/index.html:12) | VERIFIED | rg -n 'fonts.googleapis.com' jarda-ai-start/index.html |
| shared.css uses var(--serif) / var(--sans) | [`jarda-ai-start/styles/shared.css:17-18`](jarda-ai-start/styles/shared.css:17) | VERIFIED | rg -n -- '--serif\|--sans' jarda-ai-start/styles/shared.css \| head |
| 5 peers all have public evidence (site, published content) | [`docs/plans/archive/2026-04-20-discovery-plan.md:54-73`](docs/plans/archive/2026-04-20-discovery-plan.md:54), [`jarda-ai-start/docs/research/2026-04-21-round-2-research/trust-family-business-models.md:71-89`](jarda-ai-start/docs/research/2026-04-21-round-2-research/trust-family-business-models.md:71) | VERIFIED | (manual: docs/plans/archive/2026-04-20-discovery-plan.md + trust-family file read) |
| 8 SEO recipes content lives in UMBRELLA docs/plans/archive/2026-04-20-discovery-plan.md:290-345 (not submodule) | [`docs/plans/archive/2026-04-20-discovery-plan.md:290-345`](docs/plans/archive/2026-04-20-discovery-plan.md:290) | VERIFIED | sed -n '290,345p' docs/plans/archive/2026-04-20-discovery-plan.md |
| 4-archetype + Paul Zizka + 10-year-horizon content | [`jarda-ai-start/docs/research/2026-04-21-round-2-research/trust-family-business-models.md:21-150`](jarda-ai-start/docs/research/2026-04-21-round-2-research/trust-family-business-models.md:21) | VERIFIED | wc -l jarda-ai-start/docs/research/2026-04-21-round-2-research/trust-family-business-models.md |
| Growth gaps 1-9 + 4-stack revenue template | [`docs/plans/archive/2026-04-20-discovery-plan.md:77-99`](docs/plans/archive/2026-04-20-discovery-plan.md:77), [`jarda-ai-start/docs/research/2026-04-21-round-2-research/trust-family-business-models.md:134-214`](jarda-ai-start/docs/research/2026-04-21-round-2-research/trust-family-business-models.md:134) | VERIFIED | (manual) |
| Main page uses "Jay Z" reader persona (Slice 2 D5) | [`jarda-ai-start/index.html:9,27,30`](jarda-ai-start/index.html:9) | VERIFIED | rg -c 'Jay Z' jarda-ai-start/index.html |
| D11 wireframe B + D12 dossier aesthetic locked | [`jarda-ai-start/docs/plans/prds/2026-04-24-reshape/slice-2-blueprint.md:314-392`](jarda-ai-start/docs/plans/prds/2026-04-24-reshape/slice-2-blueprint.md:314) | VERIFIED (with Slice 5 additive extensions — see note below) | rg -n '^## D1[12]' jarda-ai-start/docs/plans/prds/2026-04-24-reshape/slice-2-blueprint.md |

**D11 extensions (additive, no D11 renames):** Slice 5 adds three items to wireframe B that are not in D11: (a) `<meta name="robots" content="noindex, nofollow">` in head (mirrors main page); (b) `<link rel="preconnect">` pair for fonts.googleapis.com + fonts.gstatic.com (mirrors main page); (c) `<ul class="research-sources">` inside `.research-footer` for per-page citation list (Codex R1 Blocker 2 resolution — makes `.observed` claims verifiable from the HTML). These are strict additions — no D11 element is renamed or removed. Slice 2 blueprint stays the authoritative baseline; the supplement is documented here to avoid doc/plan drift. Follow-up to update slice-2-blueprint.md itself with these additive rows is parked in Follow-ups §4 below.

## Shape Decision

Build the 4 research pages from the D11 wireframe B skeleton + D12 dossier aesthetic. Each page is Jay-Z-clean, self-contained, and follows the Observed → Inferred → May-mean → Experiment structure for every peer/section. CSS additions live at the end of `shared.css` behind a clear section comment (following the Slice 4 pattern at line 1440). Sub-slices build sequentially: CSS first, then market-clusters (longest/template validator), then the other three. Name-leak + red-flag greps run at every commit.

**Why sequential, not parallel:** Each page borrows voice from the previous. Building 5.1 → 5.2 first proves the template; 5.3–5.5 reuse the pattern. Parallel would create voice drift across pages.

**Why append CSS, not prepend:** Slice 3 extracted pre-reshape CSS verbatim (lines 1-1021); Slice 4 appended main-brief rules (1441-1616). Slice 5 continues the append pattern so each phase's contribution is grep-identifiable by section comment.

**No cross-model review.** Risk 3; reversible (local HTML/CSS, pre-push); single project. Handoff explicitly marks Codex review optional at this risk. Skipping per shape-up.md policy.

## Measurement Design

1. **What does this subsystem do?** The research pages are the "dossier" layer below the main brief — for curious readers who want the full map behind the five names in §1 and the "it depends" noted in the main page. Consumer is Jay Z (the reader persona), reading on mobile or desktop, sometimes linked-in from §6 of the main page.

2. **How will we know this made it better?** Qualitative rubric:
   - Every peer claim in `.observed` traces to public evidence.
   - Every `.inferred` reads as clearly speculative, not confident.
   - Every `.experiment` is a move Jay Z could start this week.
   - Voice matches the Phase C voice audit anchor ("Mark writing to one friend" register — minus any direct solicitation, since research pages are public).

3. **What could get worse?** (a) PII leaks into public HTML — specifically email addresses, phone numbers, home/business addresses, wife/kids names, ICO/s.r.o. registration identifiers. Guardrail: PII-pattern grep at every commit + final Slice 7 preflight. First name "Jarda" is not PII and is not gated. (b) Voice drift from main page (DHH-performed / "turns out" / "in our view"). Guardrail: red-flag denylist grep. (c) Private evidence in `.observed` blocks (claims about vendor tools a peer uses without public citation). Guardrail: Codex market-map-correction rule — `.observed` is public facts only, per [codex-cluster-1-market-map.md:205](jarda-ai-start/docs/research/2026-04-21-round-2-research/codex-cluster-1-market-map.md:205). (d) Reader-persona drift — main page uses "Jay Z"; research pages should match. Guardrail: grep `Jay Z` presence ≥ 1 in any page that names the reader.

## Acceptance Criteria

- [ ] `research/` directory exists with 4 non-empty HTML files: `market-clusters.html`, `ten-year-picture.html`, `seo-and-discovery.html`, `growth-opportunities.html`.
- [ ] Every research page head contains, in this order: `<meta charset>`, viewport meta, `<meta name="robots" content="noindex, nofollow">` (mirrors [index.html:8](jarda-ai-start/index.html:8)), `<title>`, 2 preconnect links to fonts.googleapis.com + fonts.gstatic.com (mirror [index.html:10-11](jarda-ai-start/index.html:10)), Google Fonts stylesheet `<link>`, shared.css `<link>`.
- [ ] Every research page body: `<body class="research-dossier">`, header with `.dossier-humility` line + `<h1>` + `<a href="../index.html">` back-link, `<footer class="research-footer">` containing `<ul class="research-sources">` citation list (external URLs + upstream research-file pointers as applicable). No WhatsApp / "ping me" / "reach out" solicitation on research pages — those invites belong only to the main personal-letter page.
- [ ] `market-clusters.html` contains exactly 5 `<article class="research-block">` entries (Ceranna, Avvagraphy, 2 Brides, Honest Guide, Paul Zizka), each with 4 sub-sections (`.observed`, `.inferred`, `.may-mean`, `.experiment`).
- [ ] `shared.css` gains new anchor selectors (added at end, behind `/* === Slice 5: dossier aesthetic === */` section comment): `body.research-dossier`, `body.research-dossier main`, `body.research-dossier h1`, `body.research-dossier h2`, `body.research-dossier h3`, `body.research-dossier .research-header`, `body.research-dossier .dossier-humility`, `body.research-dossier .back-link`, `body.research-dossier .observed`, `body.research-dossier .inferred`, `body.research-dossier .may-mean`, `body.research-dossier .experiment`, `body.research-dossier .research-footer`, `body.research-dossier .research-sources`. Evidence-label selectors (`.observed`, `.inferred`, `.may-mean`, `.experiment`) are ALWAYS scoped under `body.research-dossier` — no bare unscoped rules. No pre-existing selectors renamed or redefined.
- [ ] PII scan passes on all new files: no email patterns, no phone patterns (E.164 or spaced), no street-address lines, no wife/kids names carried forward from upstream docs, no Czech legal identifiers (`IČO` / `ICO`), no entity legal-form tokens (`s.r.o.`, `a.s.`, `spol. s r.o.`, `LLC`, `Ltd`, `Inc`). Public brand/domain names are fine.
- [ ] `rg -n '\b(opinionated|convention|as we say|turns out|the truth is|in our view)\b' jarda-ai-start/research/` → 0 matches.
- [ ] Every peer observation in `.observed` blocks traces to public evidence. Each page's `.research-sources` footer lists the exact URLs and/or upstream research-file paths that back up the `.observed` claims on that page.
- [ ] Word counts approximately on-budget: market-clusters **1000–1400w** body prose (5 peers × 4 blocks × ~50w + frame), ten-year-picture ~600w, seo-and-discovery **700–900w** (8 recipe lines + framing + sources), growth-opportunities ~500–700w (±20% each).
- [ ] Local browser spot-check: open `research/market-clusters.html` via `file://` — fonts render, dossier bg differs from main page, back-link works, evidence-label sections visually distinct, citation footer visible.

## Slices

### Slice 5.1 — Dossier CSS (shared.css append) [downhill]

**Demo:** `rg -n 'Slice 5: dossier aesthetic' jarda-ai-start/styles/shared.css` returns a match. All dossier rules are scoped under `body.research-dossier` (no bare `.observed` / `.inferred` / etc.). `wc -l` increases from 1617 to ~1720. No existing selectors edited.

**Files:** `jarda-ai-start/styles/shared.css`

**Steps:**
1. Append section comment block at line 1617: `/* === Slice 5: dossier aesthetic — research-page body class + scoped evidence labels === */`
2. Scoped root rules: `body.research-dossier { background: #f8f5f0; }` (or similar dossier tint — pick a value that reads as "paper" distinct from main page bg); optional `font-family: var(--serif)` for "dossier feel" per D12.
3. Scoped layout: `body.research-dossier main { max-width: 720px; margin: 0 auto; padding: 48px 24px; }` — mirrors Slice 4's content-flow sizing at [shared.css:1447](jarda-ai-start/styles/shared.css:1447).
4. Scoped heading rules: `body.research-dossier h1 / h2 / h3` — weight, size, margins matching the dossier tone (slightly quieter than main page h1/h2).
5. Dossier chrome: `body.research-dossier .research-header`, `body.research-dossier .dossier-humility` (muted italic, smaller), `body.research-dossier .back-link` (inline-safe anchor, small).
6. Evidence labels — scoped under `body.research-dossier`: `.observed`, `.inferred`, `.may-mean`, `.experiment`. Each with a visible `<h3>` label inside the section (preferred over `::before` pseudo — easier for screen readers). Distinct tint or left-border per tier so evidence level is scannable: e.g. `.observed { border-left: 3px solid var(--rule); }`, `.inferred { border-left-color: #c79b5a; }` (warning-tone), `.may-mean { border-left-color: var(--accent); }`, `.experiment { border-left-color: #4a7a53; }` (go-tone).
7. Footer: `body.research-dossier .research-footer` (centered, minimal chrome — hosts only the citation list on research pages), and `body.research-dossier .research-sources` (compact `<ul>` with small links).
8. Responsive: verify mobile rendering (no horizontal scroll, label-tier borders still visible).

**Tests:**
- All scoped selectors present: `rg -oc 'body\.research-dossier' jarda-ai-start/styles/shared.css` ≥ 13 (count of matches via `-o`, not matching lines).
- No bare evidence selectors introduced: `! rg -n '^\.(observed|inferred|may-mean|experiment)\s*\{' jarda-ai-start/styles/shared.css` (match = fail — they must be scoped).
- Section comment present: `rg -q '=== Slice 5: dossier' jarda-ai-start/styles/shared.css`.
- PII scan: `! rg -ni '(@[a-z0-9][a-z0-9.-]*\.[a-z]{2,}|\+\d{2,3}[ -]?\d{3,}|I[ČC]O[ :]*\d{5,}|\bs\.r\.o\.|\ba\.s\.\b|\bspol\. s r\.o\.|\bLLC\b|\bLtd\b|\bInc\b)' jarda-ai-start/styles/shared.css`

**Depends on:** nothing (foundation).

---

### Slice 5.2 — market-clusters.html [uphill → downhill after template proves]

**Demo:** Page renders at `file:///...research/market-clusters.html`. 5 peer articles visible. Observed / Inferred / May-mean / Experiment labels render distinct. Back-link navigates to index.html. Body prose 1000–1400w (5 peers × 4 blocks × ~50w + frame); full file `wc -w` including HTML tags 1200–1700w.

**Files:** `jarda-ai-start/research/market-clusters.html` (new).

**Content grounding (per peer — `.observed` is public-only):**
- **Ceranna Photography** — observed: Italy+CZ dual-market positioning, adventure-elopement site-wide frame, portfolio indexed by story ([docs/plans/archive/2026-04-20-discovery-plan.md:59](docs/plans/archive/2026-04-20-discovery-plan.md:59), [jarda-ai-start/index.html:180](jarda-ai-start/index.html:180)). inferred: dual-language workflow likely systematized; bilingual SEO deliberate. may-mean: same lane is available for a record-+-summit frame rather than adventure-elopement. experiment: bilingual landing page test — one post in both CZ and EN, same week, see indexation spread.
- **Avvagraphy** — observed: Prague duo, package-centric, traditional positioning ([docs/plans/archive/2026-04-20-discovery-plan.md:59](docs/plans/archive/2026-04-20-discovery-plan.md:59)). inferred: less adventure framing = different market; Prague wedding mainstream. may-mean: classical Prague market is a possible secondary lane, not primary. experiment: none — different niche, keep as reference only.
- **2 Brides / Isabelle Hesselberg** — observed: Stockholm, city-hall elopements, editorial-premium, one-lane focus ([docs/plans/archive/2026-04-20-discovery-plan.md:55](docs/plans/archive/2026-04-20-discovery-plan.md:55), [jarda-ai-start/index.html:182](jarda-ai-start/index.html:182)). inferred: picked-one-lane pattern repeats across Swedish scene. may-mean: adventure-elopement in Sweden is underserved relative to city-hall editorial. experiment: one Stockholm-vicinity adventure-elopement post with record-anchor framing.
- **Honest Guide** — observed: 2-host Prague YouTube channel (Janek Rubeš + Honza Mikulka), "local expert protects visitors" frame, warm-humor POV ([docs/plans/archive/2026-04-20-discovery-plan.md:72-73](docs/plans/archive/2026-04-20-discovery-plan.md:72)). inferred: authenticity-first brands scale slowly then compound. may-mean: "Honest Guide through the Czech / European / Scandinavian mountains" is a viable brand lens — not a tagline, a decision filter. experiment: one first-person video in the Honest Guide format (lens: no-BS, earned POV).
- **Paul Zizka** — observed: Banff, 15-year career from one place, 8 books, 23K-member community, commercial + workshops + prints + books stack ([trust-family-business-models.md:82-89](jarda-ai-start/docs/research/2026-04-21-round-2-research/trust-family-business-models.md:82)). inferred: compounding shape works; timeline is long. may-mean: 45 European peaks is the same "one place" structural bet. experiment: identify one peak that could anchor a 5-year micro-archive (book + shoots + prints + guide partnership).

**Steps:**
1. Write D11 wireframe B skeleton at `research/market-clusters.html`.
2. Head block: `<meta charset="utf-8">`, viewport, `<meta name="robots" content="noindex, nofollow">` (mirrors [index.html:8](jarda-ai-start/index.html:8)), `<title>Market &amp; peer-cluster map — research notes</title>`, 2 preconnect `<link>` tags to `fonts.googleapis.com` + `fonts.gstatic.com` (copy from [index.html:10-11](jarda-ai-start/index.html:10)), Google Fonts stylesheet `<link>` (copy from [index.html:12](jarda-ai-start/index.html:12)), shared.css `<link href="../styles/shared.css">`.
3. Body class `research-dossier`. `<header class="research-header">` contains `.dossier-humility` line + `<h1>` + `.back-link`.
4. `<main>`: 5 `<article class="research-block">` entries per content-grounding block above. Each article: `<h2>` peer name + 4 `<section>` blocks (classes `observed`, `inferred`, `may-mean`, `experiment`) each with visible `<h3>` tier-label inside.
5. `<footer class="research-footer">` containing ONLY a `<ul class="research-sources">` listing the public URLs used: Ceranna (https://ceranna.com/), Avvagraphy (https://www.avvagraphy.com/), 2 Brides (https://2brides.se/), Honest Guide (https://www.youtube.com/c/HONESTGUIDE), Paul Zizka (https://paulzizka.com/). **No "Questions about this?" or WhatsApp invite — research pages are public; solicitation belongs only on the main personal-letter page.**
6. Self-check: read aloud. Trim aggressively if over 1400w body prose.
7. Commit: `feat(reshape): Slice 5.2 — market-clusters.html (5 peers × 4-block dossier + citations)`.

**Tests:**
- `test -s jarda-ai-start/research/market-clusters.html`
- Peer article count is exactly 5: `[ "$(rg -oc 'class="research-block"' jarda-ai-start/research/market-clusters.html)" = "5" ] || echo "peer count wrong"`. (Use `-o` + `-c` so multiple classes on one line count correctly.)
- Evidence-block count is exactly 20: `[ "$(rg -o 'class="(observed|inferred|may-mean|experiment)"' jarda-ai-start/research/market-clusters.html | wc -l)" = "20" ] || echo "evidence block count wrong"`.
- `rg -q 'name="robots"\s+content="noindex' jarda-ai-start/research/market-clusters.html` (noindex required).
- `rg -q 'class="research-sources"' jarda-ai-start/research/market-clusters.html` (citation footer present).
- PII scan: `! rg -ni '(@[a-z0-9][a-z0-9.-]*\.[a-z]{2,}|\+\d{2,3}[ -]?\d{3,}|I[ČC]O[ :]*\d{5,}|\bs\.r\.o\.|\ba\.s\.\b|\bspol\. s r\.o\.|\bLLC\b|\bLtd\b|\bInc\b)' jarda-ai-start/research/market-clusters.html` (expect 0 matches; if citation URLs include `.com` domains, those won't trigger the `@` email pattern).
- `! rg -n '\b(opinionated|convention|as we say|turns out|the truth is|in our view)\b' jarda-ai-start/research/market-clusters.html`
- `rg -q 'href="../styles/shared.css"' jarda-ai-start/research/market-clusters.html`
- `rg -q 'href="../index.html"' jarda-ai-start/research/market-clusters.html`
- `rg -q 'class="research-dossier"' jarda-ai-start/research/market-clusters.html`
- No WhatsApp solicitation: `! rg -qi 'whatsapp\|ping me\|reach out\|dm me\|message me' jarda-ai-start/research/market-clusters.html`
- Word count: `wc -w jarda-ai-start/research/market-clusters.html` → 1200–1700 range (body 1000–1400w prose + HTML tag overhead ~15-20%).

**Depends on:** Slice 5.1.

---

### Slice 5.3 — ten-year-picture.html [downhill]

**Demo:** Page renders. 4 archetypes presented, Paul Zizka template detail, 10-year-horizon framing. Word count ~500–700.

**Files:** `jarda-ai-start/research/ten-year-picture.html` (new).

**Content structure (single `<article class="research-block">`, no per-peer split — this is a framework page):**
- Opening humility sentence (dossier-humility) — 1 sentence that this is imagined-forward, not earned-yet.
- `<section class="observed">` — what's observed in the archetypes:
  - 4 archetypes: Independent Reviewer, Industrial Testing, Membership, Career-Arc Photographer ([trust-family-business-models.md:21-90](jarda-ai-start/docs/research/2026-04-21-round-2-research/trust-family-business-models.md:21)).
  - Paul Zizka template: 8 books, 23K community, one specific place, family-first geography, 15 years ([trust-family-business-models.md:82-89](jarda-ai-start/docs/research/2026-04-21-round-2-research/trust-family-business-models.md:82)).
  - 6 compounding patterns ([trust-family-business-models.md:96-130](jarda-ai-start/docs/research/2026-04-21-round-2-research/trust-family-business-models.md:96)).
- `<section class="inferred">` — reading 10 years ahead for the record-+-45-peaks-+-Scandinavia angle. Compounding happens late — the last 5 years outperform the first 5 by a big margin.
- `<section class="may-mean">` — Career-Arc Photographer archetype is probably the closest fit; Paul Zizka is the single strongest template. The Kid-in-the-picture window runs in parallel.
- `<section class="experiment">` — one decision worth making now: pick the "one specific place" (probably 45-peak range or Scandinavia-adventure; don't try to own both).

**Steps:**
1. Skeleton from 5.1/5.2 pattern.
2. Write content per structure above.
3. (no call-to-action in footer — research pages are public; the "ping me" invite lives only on the main personal-letter page).

**Tests:** same grep suite as 5.2 (adapt filenames), plus:
- `rg -q 'name="robots"\s+content="noindex' jarda-ai-start/research/ten-year-picture.html`
- `rg -q 'class="research-sources"' jarda-ai-start/research/ten-year-picture.html`
- `wc -w jarda-ai-start/research/ten-year-picture.html` → 700–1000 range (~600w body + tags).

**Depends on:** Slice 5.1. (5.2 optional — for voice continuity, build after 5.2.)

---

### Slice 5.4 — seo-and-discovery.html [downhill]

**Demo:** Page renders. 8 SEO recipes listed (content copied near-verbatim from upstream; only the narrow PII set per Privacy Note below is scrubbed). Bilingual angle + 1-year moves.

**Files:** `jarda-ai-start/research/seo-and-discovery.html` (new).

**Content grounding (source: UMBRELLA [docs/plans/archive/2026-04-20-discovery-plan.md:290-345](docs/plans/archive/2026-04-20-discovery-plan.md:290)):**
- `<section class="observed">`:
  - 2026 SEO landscape: AEO > classic SEO; first 150w = answer snippet; original imagery 1.4-4.9% CTR; topical authority > keyword density; seasonal pre-staging; entity/schema helps AI citation.
  - Bilingual angle: 91 Czech podcast episodes = content goldmine ([docs/plans/archive/2026-04-20-discovery-plan.md:80](docs/plans/archive/2026-04-20-discovery-plan.md:80)); Koruna Evropy has 45 peaks, ~15 have posts → 30 long-tail targets.
- `<section class="inferred">`: AEO compounds with existing original-imagery + first-person-summit strength; the stack that wins is probably Claude + Search Console + NeuronWriter for the occasional pro-post, skip everything else.
- `<section class="may-mean">`: realistic 1-year moves — one AEO rewrite per month on existing posts, 6 new peak guides published on pre-stage calendar, image-alt batch pass.
- `<section class="experiment">`: the 8 concrete recipes (deep-linked to their cited sources — Nightwatch, Frase, SearchEngineLand, Anna Bauman, SEO Profy URLs from docs/plans/archive/2026-04-20-discovery-plan.md:293-298, preserved):
  1. AEO intro rewriter (150w answer-shape)
  2. Peak-series outline generator
  3. Seasonal publishing calendar
  4. Image alt-text + caption batch
  5. Schema markup (HowTo + Article + Person JSON-LD)
  6. Internal linking audit
  7. AI-search citation check (weekly Perplexity/ChatGPT query test)
  8. Czech podcast transcript → EN blog outline

**PRIVACY NOTE:** docs/plans/archive/2026-04-20-discovery-plan.md is an UMBRELLA (gitignored) working doc. When copying content, strip PII only: email addresses, phone numbers, home/business addresses, wife/kids names, ICO/s.r.o. identifiers. First name "Jarda" can stay (or swap to "Jay Z" for reader-persona consistency with the main page — match whichever voice the research-page body uses for other second-person references). Cite source URLs from docs/plans/archive/2026-04-20-discovery-plan.md:293-298 verbatim (they're public).

**Steps:**
1. Skeleton from 5.2 pattern.
2. Extract + rewrite 8 recipes per grounding above.
3. Source citations at bottom as `<ul>` of external links (Nightwatch, Frase, SearchEngineLand, Anna Bauman, SEO Profy) — with `target="_blank" rel="noopener"`.
4. Citation footer: `<footer class="research-footer">` containing ONLY `<ul class="research-sources">` citation list (no solicitation).

**Tests:** same grep suite as 5.2 (adapt filenames), plus:
- `rg -q 'name="robots"\s+content="noindex' jarda-ai-start/research/seo-and-discovery.html`
- `rg -q 'class="research-sources"' jarda-ai-start/research/seo-and-discovery.html`
- `rg -oc 'AEO|Answer Engine' jarda-ai-start/research/seo-and-discovery.html` ≥ 2.
- `rg -oc 'nightwatch.io|frase.io|searchengineland.com|annabauman.com|seoprofy.com' jarda-ai-start/research/seo-and-discovery.html` ≥ 3 (source citations).
- `wc -w jarda-ai-start/research/seo-and-discovery.html` → 850–1100 range (~700–900w body + tags + source URLs).

**Depends on:** Slice 5.1.

---

### Slice 5.5 — growth-opportunities.html [downhill]

**Demo:** Page renders. Structured as 3 evidence-backed anchors (lane focus, revenue mix, reader-specific moves) rather than single "Ceranna-shaped" framing. Ceranna evidence confined to the lane-focus anchor where it's actually supported.

**Files:** `jarda-ai-start/research/growth-opportunities.html` (new).

**Framing note (per Codex R1 — Ceranna evidence is thin for a full-page frame):** Use a 3-section structure, each `<article class="research-block">` with its own evidence anchor and full 4-tier Observed→Inferred→May-mean→Experiment treatment. Ceranna anchors section 1 only. §6 pointer label at [index.html:240](jarda-ai-start/index.html:240) reads "Ceranna-shaped segment moves" — this page delivers on that promise by showing where Ceranna IS the right anchor (lane focus) and naming the other anchors (Zizka, loudavymkrokem) where different evidence is sturdier. Pointer label stays untouched (no Slice 4 edit).

**Content grounding (per [docs/plans/archive/2026-04-20-discovery-plan.md:77-99](docs/plans/archive/2026-04-20-discovery-plan.md:77) growth gaps + [trust-family-business-models.md:134-214](jarda-ai-start/docs/research/2026-04-21-round-2-research/trust-family-business-models.md:134)):**

**Section 1 — Lane focus (Ceranna anchor):**
- `.observed`: Italy + CZ dual-market, adventure-elopement site-wide frame, portfolio indexed by story not venue, bilingual content parallel-published ([docs/plans/archive/2026-04-20-discovery-plan.md:59](docs/plans/archive/2026-04-20-discovery-plan.md:59)).
- `.inferred`: lane-commitment compounds — one "pick and stay" move beats three half-committed lanes.
- `.may-mean`: for the reader, "lane" = record + summit + Scandinavia-adventure. Everything else is secondary.
- `.experiment`: one landing page reframed around the lane (record-anchored), one CZ post + one EN post both published same week on the same topic.

**Section 2 — Revenue mix (Zizka + loudavymkrokem anchors):**
- `.observed`: 4-stack revenue template ([trust-family-business-models.md:204-214](jarda-ai-start/docs/research/2026-04-21-round-2-research/trust-family-business-models.md:204)). CZ-market validation: loudavymkrokem.cz 5-stream, 120-150K CZK/mo ad revenue ([trust-family-business-models.md:216-221](jarda-ai-start/docs/research/2026-04-21-round-2-research/trust-family-business-models.md:216)). Zizka's Banff version: 8 books + commercial + workshops + prints + 23K-member community ([trust-family-business-models.md:82-89](jarda-ai-start/docs/research/2026-04-21-round-2-research/trust-family-business-models.md:82)). 10 revenue channels catalogued with effort/ceiling ([trust-family-business-models.md:134-150](jarda-ai-start/docs/research/2026-04-21-round-2-research/trust-family-business-models.md:134)).
- `.inferred`: compounding-stack works; the sequence matters (prints before membership, books before commercial).
- `.may-mean`: a 3-year shape that starts with prints + affiliates, layers workshops + digital products at year 2, membership at year 3.
- `.experiment`: first new revenue stream — one Rexby guide (e.g. "Crown of Europe summit routes") using existing Koruna Evropy content. Low-risk digital product, cross-promotes the book.

**Section 3 — Reader-specific moves (growth-gaps anchor):**
- `.observed`: discovery-plan growth gaps list — funnel integration, language repurposing (91 CZ podcast episodes), record visibility, anniversary engine, book-to-leads, SEO cadence, IG-to-long-form bridge ([docs/plans/archive/2026-04-20-discovery-plan.md:77-99](docs/plans/archive/2026-04-20-discovery-plan.md:77)).
- `.inferred`: each gap is a compounding lever — language repurposing is the biggest because content already exists.
- `.may-mean`: the reader's 12-month ROI looks like 3-5 of these gaps closed, not all 9.
- `.experiment`: one concrete move for week 1 — anniversary-engine email nurture drafted by Cowork against past-client list ([docs/plans/archive/2026-04-20-discovery-plan.md:82](docs/plans/archive/2026-04-20-discovery-plan.md:82)). One prompt, quick feedback loop.

**Citation footer (`.research-sources`):** discovery-plan archive path (internal), trust-family-business-models.md (internal), loudavymkrokem.cz (public), Rexby (https://www.rexby.com/), Paul Zizka community (https://paulzizka.com/).

**Steps:**
1. Skeleton from 5.2 pattern.
2. Three `<article class="research-block">` entries per content grounding above. Each article has `<h2>` section title + 4 evidence sections.
3. Citation footer (`.research-sources` only — no solicitation).

**Tests:** same grep suite as 5.2 (adapt filenames), plus:
- `rg -q 'name="robots"\s+content="noindex' jarda-ai-start/research/growth-opportunities.html`
- `rg -q 'class="research-sources"' jarda-ai-start/research/growth-opportunities.html`
- `[ "$(rg -oc 'class="research-block"' jarda-ai-start/research/growth-opportunities.html)" = "3" ] || echo "section count wrong"`.
- `[ "$(rg -o 'class="(observed|inferred|may-mean|experiment)"' jarda-ai-start/research/growth-opportunities.html | wc -l)" = "12" ] || echo "evidence block count wrong (expect 12 = 3×4)"`.
- `wc -w jarda-ai-start/research/growth-opportunities.html` → 800–1100 range (~600–700w body + tags).

**Depends on:** Slice 5.1.

---

## Existing Patterns

- **Section comment pattern for shared.css** — follow Slice 4's pattern at [shared.css:1440-1445](jarda-ai-start/styles/shared.css:1440): `/* === Slice N: descriptive-name === */` with a blank line before and after.
- **Google Fonts `<link>`** — copy verbatim from [index.html:12](jarda-ai-start/index.html:12). Every research page head includes it before the shared.css link.
- **Peer-sketch voice pattern** — match tone from [index.html:180-184](jarda-ai-start/index.html:180) (current §4.1). 3-5 sentences per peer, factual + one inference marker ("the pattern is", "the shape is").
- **Dossier humility clause** — per D11 wireframe B: "Surface-level scan. Written by Mark, desk-research not field-research — where I'm guessing vs. where I have evidence is flagged per block." This exact line at page top (or a close paraphrase per page).
- **Research-page footer convention** — main page uses a WhatsApp ping-me closer at [index.html:247](jarda-ai-start/index.html:247), appropriate because it's a personal letter. Research pages are public documents anyone can land on; the footer should NOT solicit contact. Keep only `.research-sources` inside `.research-footer`.
- **`../` prefix** — research pages are one directory deep; all asset links use `../` prefix.

## What This Replaces

Nothing. Pre-reshape site had no `/research/` directory. Slice 4 added dead hrefs at [index.html:237-240](jarda-ai-start/index.html:237) pointing forward to this slice. After Slice 5, those hrefs resolve.

## No-Gos

- **Do NOT** rename, redefine, or touch pre-reshape selectors in shared.css (specifically `.research-block` at line 1246). D12 is move-not-rewrite.
- **Do NOT** copy PII from umbrella `docs/plans/archive/2026-04-20-discovery-plan.md` or any other upstream doc: email addresses, phone numbers, home/business addresses, wife/kids names, ICO numbers, s.r.o. legal names. First name "Jarda" is not PII and is not blocked. Public brand names (`korunaevropy.cz`, `thebestviewpoints.com`) are fine.
- **Do NOT** put private or speculative claims in `.observed` blocks. Observed = public evidence only.
- **Do NOT** add a 5th research page, refactor existing CSS, or extend index.html. Contract fences: 4 pages + CSS append only.
- **Do NOT** invoke cross-model (Codex/Gemini) review. Risk 3 + reversible + single project → optional per shape-up.md, and handoff says skip for Slice 5.
- **Do NOT** push to origin. Slice 7 handles push-time privacy preflight.
- **Do NOT** mark Slice 6 (proofread) or Slice 7 (ship) complete in this slice. Scope is HTML + CSS build only.

## Verification Commands

Run the full suite after Slice 5.5 commit, before marking Slice 5 complete:

```bash
cd jarda-ai-start

# 1. All 4 pages exist + non-empty
for p in market-clusters ten-year-picture seo-and-discovery growth-opportunities; do
  test -s "research/$p.html" || echo "MISSING: $p"
done

# 2. PII scan (regex covers emails, E.164 phones, CZ legal identifiers, entity legal-form tokens).
#    First name "Jarda" is NOT PII and not blocked. Public brand names (korunaevropy.cz, thebestviewpoints.com) are fine — they do not match `@domain` (email) pattern.
! rg -ni '(@[a-z0-9][a-z0-9.-]*\.[a-z]{2,}|\+\d{2,3}[ -]?\d{3,}|I[ČC]O[ :]*\d{5,}|\bs\.r\.o\.|\ba\.s\.\b|\bspol\. s r\.o\.|\bLLC\b|\bLtd\b|\bInc\b)' research/ styles/shared.css
# Visual read of each page for: wife/kids names, home/business addresses, referral codes — greps are weak on these categories.

# 3. Every page links stylesheet correctly
for p in research/*.html; do
  rg -q 'href="../styles/shared.css"' "$p" || echo "MISSING stylesheet link: $p"
done

# 4. Every page has body.research-dossier
for p in research/*.html; do
  rg -q 'class="research-dossier"' "$p" || echo "MISSING dossier body class: $p"
done

# 5. Every page has Google Fonts link + both preconnect domains
for p in research/*.html; do
  rg -q 'href="https://fonts.googleapis.com/css' "$p" || echo "MISSING Google Fonts stylesheet: $p"
  rg -q 'preconnect.*fonts\.googleapis\.com' "$p" || echo "MISSING preconnect to fonts.googleapis.com: $p"
  rg -q 'preconnect.*fonts\.gstatic\.com' "$p" || echo "MISSING preconnect to fonts.gstatic.com: $p"
done

# 6. Every page has noindex meta (mirror of main page policy)
for p in research/*.html; do
  rg -q 'name="robots"\s+content="noindex' "$p" || echo "MISSING noindex meta: $p"
done

# 7. Every page has a citation footer
for p in research/*.html; do
  rg -q 'class="research-sources"' "$p" || echo "MISSING .research-sources footer: $p"
done

# 8. Red-flag voice grep
! rg -n '\b(opinionated|convention|as we say|turns out|the truth is|in our view)\b' research/

# 9. NO solicitation on research pages (WhatsApp/ping-me/etc. are for the main personal-letter page only)
for p in research/*.html; do
  ! rg -qi 'whatsapp|ping me|reach out|dm me|message me|drop me a line' "$p" || echo "FAIL (unwanted solicitation): $p"
done

# 10. Back-link to main page
for p in research/*.html; do
  rg -q 'href="../index.html"' "$p" || echo "MISSING back-link: $p"
done

# 11. market-clusters has 5 peer articles × 4 evidence blocks (use -o for accurate counts)
[ "$(rg -oc 'class="research-block"' research/market-clusters.html)" = "5" ] || echo "market-clusters peer count wrong"
[ "$(rg -o 'class="(observed|inferred|may-mean|experiment)"' research/market-clusters.html | wc -l | tr -d ' ')" = "20" ] || echo "market-clusters evidence-block count wrong (expect 20)"

# 12. growth-opportunities has 3 sections × 4 evidence blocks
[ "$(rg -oc 'class="research-block"' research/growth-opportunities.html)" = "3" ] || echo "growth-opportunities section count wrong"
[ "$(rg -o 'class="(observed|inferred|may-mean|experiment)"' research/growth-opportunities.html | wc -l | tr -d ' ')" = "12" ] || echo "growth-opportunities evidence-block count wrong (expect 12)"

# 13. shared.css gained Slice 5 section + scoped rules (no bare evidence selectors)
rg -q '=== Slice 5: dossier' styles/shared.css || echo "MISSING Slice 5 section comment"
[ "$(rg -oc 'body\.research-dossier' styles/shared.css)" -ge "13" ] || echo "shared.css dossier selector count too low"
! rg -n '^\.(observed|inferred|may-mean|experiment)\s*\{' styles/shared.css || echo "FAIL: bare (unscoped) evidence selector in shared.css"

# 14. Word counts (rough — HTML tags add overhead; check body prose ≈ per-page budget)
for p in research/*.html; do
  echo "$p: $(wc -w < "$p") words (incl HTML)"
done

# 15. Visual spot-check (manual): open each page in browser
# open research/market-clusters.html research/ten-year-picture.html research/seo-and-discovery.html research/growth-opportunities.html
```

If any check fails, fix-in-place and re-run before marking Slice 5 complete.

## Ship boundary (explicit)

Slice 5 ends at commit of Slice 5.5 with all verification commands passing. Slice 6 (proofread, incl. full doc re-read per voice-audit) and Slice 7 (ship to origin/main + GitHub Pages verify + Jay Z handoff) are scoped separately in the handoff. **Do not push to origin in this slice.**

## Follow-ups (out of Slice 5 scope)

1. **README.md privacy-policy wording refresh** — [README.md:5-7](jarda-ai-start/README.md:5) says "real name, real URLs, and real referral codes never land here." The 2026-04-24 policy clarification is narrower: real URLs + referral codes still excluded; first name "Jarda" is fine. Soften the README line to reflect that (candidate: Slice 6 or a tiny standalone S-slice). No Slice 5 action.

2. **§6 pointer label refinement (optional)** — [index.html:240](jarda-ai-start/index.html:240) says "Growth opportunities — Ceranna-shaped segment moves". Slice 5.5 delivers Ceranna as one of three anchors (not the sole frame). If that reads as a broken promise, the pointer could be softened to "Growth opportunities — lane focus, revenue mix, reader-specific moves". Candidate: Slice 6 polish pass. Not Slice 5 scope.

3. **Full-page citation mechanism in wireframe A** — Slice 5 introduces `.research-sources` on dossier pages. If this pattern works well, the main page may benefit from a similar consolidated citation list. Bench/Slice 6 triage.

4. **slice-2-blueprint.md D11 additive rows** — Slice 5 extends D11 wireframe B with 3 additive elements (noindex meta, preconnect pair, `.research-sources` footer). These are documented here but not yet backfilled into the authoritative D11. When Slice 6 / 7 touches the blueprint for its own reasons, append additive rows to D11 with the 2026-04-24 timestamp so the blueprint and Slice 5 reality converge. Small — ~5 lines of markdown.
