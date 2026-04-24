---
ticket: jarda#reshape-2026-04-23
status: active
appetite: L
risk_score: 6
project: jarda-ai-start
updated: 2026-04-24
parent: docs/plans/2026-04-23-jarda-reshape-refresher-primer.md
shaping: true
files:
  - jarda-ai-start/docs/plans/prds/2026-04-24-reshape/slice-2-blueprint.md
---

# Slice 2 Blueprint — Reshape refresher-primer

## Problem

The current `jarda-ai-start/index.html` (6 Stops × 3 Blocks e-learning frame + 24 go-deeper drawers) fights the one-reader, WhatsApp-register brief that Slice 1 research now supports. Three reviewer lenses converged: identity arrives 12–14 min in (C2), the counter chrome signals LMS-grade workload (C1), voice drifts to DHH aphorism (C3), the research appendix reads as raw homework (C4), and 24 hidden drawers bury identity payload (C5). Slice 1 shipped 10/10 research deliverables; the reshape is now a sequencing + voice + IA problem, not an information problem. Slice 2's job is to lock every pre-build decision in one signed contract so Slices 3–7 (CSS extraction, main page build, research pages, proofread, ship) run as mechanical execution — not re-shaping in disguise.

One concrete failure state: if Jarda opens the current site on Friday before his cowork AI session and skims for 5 minutes, the first genuinely Jarda-specific thing he sees (the peer-cluster map of Ceranna / Avvagraphy / 2 Brides / Honest Guide / Paul Zizka) does not appear — it's below the fold, past generic Jeff Su re-explanation, and gated behind four drawers. He leaves with the `Stop 1 of 6 · Block 1 of 3` feeling that the site is homework, not a gift from Mark.

## Verified Assumptions

| Claim | Source | Status | Verified At | Verify |
|-------|--------|--------|-------------|--------|
| Slice 1 produced the research vault at `docs/research/2026-04-24-reshape-research/` containing voice-audit, video-companion-drafts, line-by-line UXR synthesis, personal-brief-patterns, and spikes A/B | [docs/research/2026-04-24-reshape-research/voice-audit.md](docs/research/2026-04-24-reshape-research/voice-audit.md) | VERIFIED | 2026-04-23T22:43:26-05:00 | test -f docs/research/2026-04-24-reshape-research/voice-audit.md && test -f docs/research/2026-04-24-reshape-research/video-companion-drafts.md && test -f docs/research/2026-04-24-reshape-research/line-by-line-ux-review.md && test -f docs/research/2026-04-24-reshape-research/personal-brief-patterns.md |
| `voice-audit.md` includes 3 sample pairs ready for blueprint consumption (Pair 1 Cowork projects, Pair 2 first-week habit, Pair 3 ten-year picture) | [docs/research/2026-04-24-reshape-research/voice-audit.md:270](docs/research/2026-04-24-reshape-research/voice-audit.md) | VERIFIED | 2026-04-23T22:43:26-05:00 | rg -q "^### Pair 1" docs/research/2026-04-24-reshape-research/voice-audit.md && rg -q "^### Pair 2" docs/research/2026-04-24-reshape-research/voice-audit.md && rg -q "^### Pair 3" docs/research/2026-04-24-reshape-research/voice-audit.md |
| `video-companion-drafts.md` contains 4 locked companions (Jeff Su, Jack Roberts, Jesse Genet a16z, Jesse Genet Cognitive Revolution) with master-section tables + timestamps + summaries | [docs/research/2026-04-24-reshape-research/video-companion-drafts.md:3,34,68,108](docs/research/2026-04-24-reshape-research/video-companion-drafts.md) | VERIFIED | 2026-04-23T22:43:26-05:00 | rg -q "Jeff Su" docs/research/2026-04-24-reshape-research/video-companion-drafts.md && rg -q "Jack Roberts" docs/research/2026-04-24-reshape-research/video-companion-drafts.md && rg -q "Jesse Genet .a16z" docs/research/2026-04-24-reshape-research/video-companion-drafts.md && rg -q "Cognitive Revolution" docs/research/2026-04-24-reshape-research/video-companion-drafts.md |
| Line-by-line UXR synthesis has 5 convergent findings (C1–C5) from 3 reviewer lenses (Codex / Gemini / Explore) | [docs/research/2026-04-24-reshape-research/line-by-line-ux-review.md:15,21,27,33,39](docs/research/2026-04-24-reshape-research/line-by-line-ux-review.md) | VERIFIED | 2026-04-23T22:43:26-05:00 | rg -q "^### C1\." docs/research/2026-04-24-reshape-research/line-by-line-ux-review.md && rg -q "^### C5\." docs/research/2026-04-24-reshape-research/line-by-line-ux-review.md |
| Spike C (personal-brief patterns) documents the N=1 override map for Spike A (e-learning) and Spike B (exec-summary) | [docs/research/2026-04-24-reshape-research/personal-brief-patterns.md:54](docs/research/2026-04-24-reshape-research/personal-brief-patterns.md) | VERIFIED | 2026-04-23T22:43:26-05:00 | rg -q "^## Override map" docs/research/2026-04-24-reshape-research/personal-brief-patterns.md |
| Umbrella plan Slice 2 scope (Blueprint + wireframes + vocabulary + voice) is defined at L224 of parent plan | [docs/plans/2026-04-23-jarda-reshape-refresher-primer.md:224](docs/plans/2026-04-23-jarda-reshape-refresher-primer.md) | VERIFIED | 2026-04-23T22:43:26-05:00 | rg -q "^### Slice 2 — Blueprint" docs/plans/2026-04-23-jarda-reshape-refresher-primer.md |
| Current `index.html` carries e-learning "Stop N of 6" / "Block N of X" chrome that Slice 2 must decide how to replace | [index.html](index.html) | VERIFIED | 2026-04-23T22:43:26-05:00 | rg -q "Stop [1-6] of 6" index.html && rg -q "Block [1-4] of" index.html |
| Current `index.html` carries 24 `branch-drawer` entries (6 stops × 4 branches) with `Go deeper` labels (Slice 2 D10 audit target) | [index.html](index.html) | VERIFIED | 2026-04-23T23:03:51-05:00 | rg -q 'class="branch-drawer"' index.html && rg -q "Go deeper" index.html |

## Shape Decision

Lock 12 decisions that collectively determine the shape of main + research pages and unblock Slices 3–7. Each decision documents the research inputs, the call, and the trade-off. Where the N=1 Spike C override conflicts with Spike A (e-learning) or Spike B (exec-summary), C wins per umbrella plan governance. Where reviewer lenses diverged (line-by-line synthesis D1–D3), resolutions from the synthesis doc are applied verbatim.

### D1 — Structure: single-page main + sibling research pages (no `/practical/`)

**Decision.** Main page is single-page progressive (`/index.html`, §1–§6). Deeper research lives on 3–4 sibling pages at `/research/<topic>.html`. No `/practical/` sibling — practical guidance stays inline in §5 of main.

**Research inputs.** Line-by-line synthesis D1 (divergence: Codex wanted split, Gemini/Explore wanted single-page). Resolution doc (synthesis:51) reads: "Keep single-page progressive as the working assumption; the teaser-forward ordering IS the Codex mode-switch in disguise." Spike C (personal-brief patterns): a letter flows, doesn't fork.

**Why.** The single-page flow honors the WhatsApp-register anchor (Spike C) — a letter doesn't get paginated. The research-page separation IS justified per C4 (research appendix reads as "raw homework" currently; a visible wrapper change plus evidence labeling turns it into a dossier). The `/practical/` sibling was speculative in the umbrella plan pending Slice 1 output; Slice 1 Spike C says practical guidance is part of the letter, not a separate surface. One fewer moving part.

**Trade-off.** The single-page flow risks length fatigue. Mitigation: ~20-minute skim budget enforced by the opening-90s contract (§1) and the exec-summary brief (§4) both being scannable. Go-Deeper audit (D10) cuts ornamental drawers that inflate perceived length.

### D2 — Section ordering: teaser-forward (not canonical)

**Decision.** Order is §1 Opening (the teaser) → §2 AI right now → §3 Cowork world right now → §4 The brief → §5 First-week practice → §6 Deeper research pointers. The §1 opening carries the 90-second contract + Jarda-named addressing + peer-cluster teaser (names only, no analysis) before §2–§3 expose Jeff Su / Jack Roberts / Jesse Genet content.

**Research inputs.** Line-by-line synthesis hook #5: "three-reviewer convergence on 'peer-map arrives too late' is strong evidence for the teaser-forward variant over canonical ordering." C2 finding (identity arrives too late) confirmed by all three reviewer lenses. Umbrella plan L165–170 named this as an ordering variant to decide in Slice 2.

**Why.** Identity → action compass wins. The teaser-forward variant IS the Codex "hard mode-switch" argument folded into a single-page layout (synthesis D1 resolution). Canonical ordering (AI-first, then Cowork, then brief) re-commits the C2 error.

**Trade-off.** Risk: reader reaches §2 and expects the AI/Cowork section to re-prove the teaser's claims before being ready to trust the §4 brief. Mitigation: §2–§3 are scannable companion summaries (memory-trigger for learning videos, stand-alone for interview videos per umbrella plan 70/30 rule at L133–134), not proof obligations.

### D3 — Vocabulary: kill `Stop N of 6` and `Block N of 3` outright; no replacement

**Decision.** No "Stop" label. No "Block" label. No "Lesson / Module / Section" substitutes. Sections are named by what they contain (e.g., "What's actually different about Cowork", "The brief I promised"). Ordinal anchoring only via section titles + a thin progress line in the header (Gemini recommendation).

**Research inputs.** C1 finding (three-lens convergence: "Stop N of 6 · Block N of 3" is e-learning chrome that fights the frame). Spike C override map (personal-brief-patterns.md:56–62): "A letter doesn't have lessons. If Spike A recommends e-learning's pedagogical chunking labels, N=1 replaces them with what a friend would actually call the pieces … or no label at all." Spike A alone suggested "Lesson" as the universal term; Spike C N=1 overrides.

**Why.** The current `Stop` counter is already lying (4-block stops exist; synthesis:19 notes "3/3/3/4/4/4 blocks across the six stops"). Any surviving counter vocabulary pulls identity toward LMS, not toward "friend sending me a note." "No label" reads as the register a WhatsApp voice note would adopt.

**Trade-off.** Loss of wayfinding signal. Mitigation: thin progress line + section titles descriptive enough to anchor without ordinals. Accepts that skim readers lose "percent complete" gauge; gains that no reader feels they're doing homework.

### D4 — Voice posture + 3 sample pairs

**Decision — voice guidance (1 paragraph).** Voice anchor is Mark writing to one friend over WhatsApp. First person throughout (present, not just at edges). Second person is Jarda specifically, not "you the reader." No aphorisms, no 37signals / DHH cadence, none of: `opinionated`, `convention`, `as we say`, `turns out`, `the truth is`, `in our view`. When a thought generalizes, let it generalize — don't perform intimacy that isn't earned. Reader-texture (named details about Jarda's situation — Ceranna, Jesse, the cowork, the book) appears sparingly and causally: each reference earns its place because it proves attentive reading (Rilke pattern per personal-brief-patterns.md:29–34). Decisiveness is in-register (Rilke told Kappus to stop writing love poems; that's the register, not hedging). Humility clause appears twice around §4 — framing + invitational — per D9.

**Three sample pairs** (imported verbatim from [voice-audit.md:270–283](../../../research/2026-04-24-reshape-research/voice-audit.md)):

**Pair 1 — on Cowork projects (§3 territory)**
- *Doesn't sound like*: "A project is where Cowork stops forgetting. Drop a one-page 'who I am, what I do' into a project, add any reference files, and every new chat in that project starts with that context. Every conversation after is faster. Projects earn their setup cost when the context will be reused; under that threshold, the ceremony slows you down."
- *Sounds like*: "A project is basically the place where Cowork finally remembers you. You drop a short 'who I am, what I do' file in, plus any reference stuff you've got, and every new chat in that project starts already knowing it. Worth setting one up when you'll reuse the context — otherwise plain chat's fine, don't overcomplicate it."

**Pair 2 — on the first-week habit (§5 territory)**
- *Doesn't sound like*: "The first-week habit is smaller than it looks. After a recurring piece of work — a call, a session, a task that keeps coming back — drop a short note into Cowork. Text, a photo, thirty seconds of voice, whichever costs least friction. Don't sit at the laptop for it. A habit that requires sitting down doesn't survive week one. The habit costs less than the ambition to keep it. That is the point."
- *Sounds like*: "Honestly the first-week habit is pretty small. After something you do regularly — a shoot, a call, a booking back-and-forth — just drop a quick note into Cowork. Thirty seconds of voice, a photo, whatever's easiest. Don't make yourself sit at the laptop or you won't do it past day three. The whole idea is making it cheap enough that you actually keep it up."

**Pair 3 — on the ten-year picture (§6 / research territory)**
- *Doesn't sound like*: "The creator whose work most closely rhymes with where you could go is Paul Zizka. Not a celebrity — a specialist who compounded. Specificity beats breadth. Your particular mix is already the thing. No need to broaden. Say no to anything you wouldn't recommend for free. Trust compounds slowly. The first cheap partnership is what kills credibility at year seven."
- *Sounds like*: "The closest comparison I could find for where you could end up is Paul Zizka — a mountain photographer who built a whole career from one specific place over about fifteen years. Not a famous name, just someone who kept stacking work. Your mix — the book, the guiding, being bilingual — is already pretty specific, you probably don't need to widen it. And the one pattern that shows up across all the people I looked at: they say no to stuff they wouldn't recommend for free, because the cheap partnerships are what mess up the trust years later."

Pairs 1, 2, 3 each include the DHH-performed counter-sample ("Doesn't sound like") — synthesis C3 target phrases (`Trust is earned per permission`, `The notes are boring`, `Specificity beats breadth`, `clever prompting ages out`, the Stop-5 aphorism) are absorbed into the "doesn't sound like" column of Pair 3 ("Specificity beats breadth" + "Trust compounds slowly").

### D5 — Opening-90s contract (drafted copy, ~175 words)

**Order.** who+why → what → payoff. (Per umbrella plan L170 hypothesis — teaser-forward naming Jarda, then stakes, then deliverables.)

**Draft copy** (locked in Slice 2, proofread in Slice 6):

> Hi Jarda,
>
> This is for you. Jesse asked me to map out what I've been seeing in AI + the cowork world — where it touches your ten-year picture, what I'd actually pay attention to this year, and where I think the opening is. You've already watched Jeff Su and Jack Roberts, so I'm not re-explaining what Cowork is; this picks up from there.
>
> A few things I want you to leave with: five names — **Ceranna, Avvagraphy, 2 Brides, Honest Guide, Paul Zizka** (full map is in §4) — one first-week habit I think is a real unlock, and my best guess at the one-sentence brief for where your market is going.
>
> The Jeff Su and Jack Roberts sections below are mostly refresher — skim or skip. Jesse Genet is new, I'd read those. If you want the brief first, jump straight to §4; the videos will still be there after.
>
> You can skim this in 20 minutes. Deeper research is parked in a separate folder — link at the end. WhatsApp is best for follow-ups.
>
> —M

**Word count.** ~175 words. **Red-flag grep.** Zero matches for `opinionated|convention|as we say|turns out|the truth is|in our view` when scoped to blockquote lines (`^> `) — the denylist tokens appear elsewhere in this PRD as meta-documentation (this paragraph names them; the voice guidance in D4 lists them), so the grep must target drafted copy only. Verification command in §Verification Commands uses `^> ` prefix.

### D6 — Master-section titles + timestamps locked per video

All four companion tables are final (per Slice 1 deliverable at [video-companion-drafts.md](../../../research/2026-04-24-reshape-research/video-companion-drafts.md)). Slice 4 (build) consumes these directly.

| Video | Type | Duration | Section count | Treatment |
|-------|------|----------|---------------|-----------|
| Jeff Su — z9rdrNrkvDY | learning | ~19 min | 4 | Memory-trigger ~150w summary above video (70/30 rule — learning side) |
| Jack Roberts — cNf7uVff11Y | learning | ~65 min | 7 | Memory-trigger ~150w summary above video (70/30 rule — learning side) |
| Jesse Genet (a16z) — yiJOTCRVWjc | interview | ~54 min | 5 | Stand-alone ~290w summary + 2–3 load-bearing quotes (70/30 rule — interview side) |
| Jesse Genet (Cognitive Revolution) — aFQskhdR3RQ | interview | ~126 min | 6 | Stand-alone ~295w summary + 2–3 load-bearing quotes (70/30 rule — interview side) |

Section titles and start-end timestamps per companion are authoritative as written in video-companion-drafts.md; Slice 4 must not re-draft or re-title them without Slice 2 re-shape.

### D7 — IA blueprint (section-by-section outline + draft copy)

| § | Title (working) | Purpose | Length budget | Drafted in Slice 2? |
|---|------------------|---------|---------------|---------------------|
| §1 | Opening (teaser) | Jarda-named addressing, 90s contract, peer-cluster teaser (names inline) + mode-switch sentence (jump to §4) + video skim guidance | ~175w contract + ~95w intro = ~270w | YES (D5 + §1 intro below) |
| §2 | AI right now | Jeff Su + Jack Roberts companions (memory-trigger ~150w each above video) | 2 × ~150w = ~300w | Slice 1 content (copy in [video-companion-drafts.md](../../../research/2026-04-24-reshape-research/video-companion-drafts.md)) |
| §3 | Cowork world right now | Jesse Genet ×2 companions (stand-alone ~290w + ~295w + load-bearing quotes) | ~600w | Slice 1 content (copy in [video-companion-drafts.md](../../../research/2026-04-24-reshape-research/video-companion-drafts.md)) |
| §4 | The brief | Exec-summary of my own analysis; humility clause top + end | ~850w (per D8 breakdown) | Handoff copy drafted below; sub-section body copy → Slice 4 |
| §5 | First-week practice | One habit, one setup, one project; inline (not drawered) | ~250–350w | Body copy → Slice 4 |
| §6 | Deeper research | Pointers to `/research/*.html` pages, one-line rationale each | ~150w | Pointer list → Slice 4 |

**Draft intro copy** (top of §1, after the 90s contract, ~95w):

> Everything below is how I got to the five names and the one sentence. I'll start with what the AI and Cowork world looks like right now (Jeff + Jack for what Cowork actually is, Jesse for what people are building with it when they stop being impressed and start shipping). Then my own read on where Ceranna sits and what I'd do in your first week. The deeper research — market map, peer cluster, SEO, long-range scenarios — is parked in a folder at the end. Skim what you need; ignore what you don't.

**Draft business-brief handoff copy** (transition into §4, ~110w, carries humility clause TOP per D9):

> Here's the part I actually wrote for you. The videos above are scaffolding — useful, but someone else already said it. This section is my read: what I see in your segment of the cowork-adjacent photography market, why I think the door is open now, and what a first serious move would look like if it were me. I might be wrong. I've flagged the places where I'm guessing. If any of it lands wrong — the segment I picked, the time horizon, the move — please push back. The working version is more useful than a polished version I have to defend later.

Red-flag grep on both drafted blocks (blockquote-scoped, `^> ` prefix): zero matches.

### D8 — Exec-summary brief outline (§4 sub-sections)

| Sub-section | Purpose | Word budget |
|-------------|---------|-------------|
| 4.1 — Where the market actually is | Peer cluster (Ceranna / Avvagraphy / 2 Brides / Honest Guide / Paul Zizka); what each is doing; what that tells us about the shape of Jarda's segment | ~250w |
| 4.2 — What's moving | The trend or opening I think matters — copywriting constraint: thesis must be anchored on evidence from the 4.1 peer-cluster treatment (not a free-standing prediction). Candidate theses (author picks one in Slice 4): AI-adjacent service premium / agency shift / platform consolidation. Whichever thesis Slice 4 drafts, it must cite ≥2 peer-cluster names from 4.1 as grounding. | ~200w |
| 4.3 — What I'd do first | The one concrete move, specific enough to act on Monday | ~250w |
| 4.4 — Where I might be wrong | Honest uncertainty; what would change my read; humility clause END (per D9) | ~150w |

**Total §4.** ~850w. Skim budget: 3–4 minutes inside the ~20-minute overall target.

**Sub-section order locked:** 4.1 → 4.2 → 4.3 → 4.4. Rationale: 4.1 provides evidence that 4.2 cites; 4.3 depends on the 4.2 thesis; 4.4 must close §4 (humility placement B is at section close per D9 — any other order would put the closing humility clause mid-section). Slice 4 build has zero re-ordering authority; word budgets + humility placements are contract-level locked.

### D9 — Humility clause at TWO placements (top + end of §4)

**Placement A — TOP of §4 (inside the business-brief handoff copy drafted in D7):**

> "I might be wrong. I've flagged the places where I'm guessing. If any of it lands wrong — the segment I picked, the time horizon, the move — please push back."

This sits inside the ~110w D7 handoff block and frames the brief before reader reaches 4.1.

**Placement B — END of §4 (inside 4.4 "Where I might be wrong"):**

> "If your read differs, I'd rather hear it now — a working version is more useful than a polished one I have to defend later. WhatsApp, whenever."

This closes §4 with an explicit invitation and the WhatsApp anchor (which is also the footer-fix target per line-by-line synthesis hook #7).

**Why split, not single.** Synthesis + umbrella plan hypothesis (L245–247): single-instance humility reads as throat-clearing (unearned ritual); split reads as honest framing on the way in + invitation on the way out. The two placements do different jobs (frame vs invite) and neither is substitutable for the other.

**Trade-off.** Risk: two humility moves in one section read as hedging. Mitigation: placement A is active ("I might be wrong — push back"), placement B is procedural ("WhatsApp, whenever"). Different verbs, different functions.

### D10 — Go-Deeper audit criterion: "Would Jarda, specifically, click this?"

**Criterion.** For each current go-deeper drawer/chip, answer: *Would Jarda, specifically, click this in a 20-minute skim? AND does the branch carry identity-payload (something specific to his situation) or action-payload (a concrete next step)?* Both must be YES. Generic-depth branches are killed. Ornamental drawers (nice-to-knows that don't change what he does) are killed.

**Expected kill rate.** ≥80% (three-lens convergence per C5 resolution in synthesis).

**Full drawer inventory audit (locked here, not deferred).** Current site has 24 drawers: 6 stops × 4 branches (Personal / Creative / Client / Deeper — confirmed at [`index.html:1538–1541`](../../../../index.html), pattern repeats at stops 2–6). All four axis labels are generic — they chunk by *hypothetical audience type* (any reader who identifies as Personal-oriented, Creative-oriented, Client-oriented, or wants to go Deeper), not by Jarda-specific identity or action. Per the D10 criterion (both identity AND action must be YES), **all 24 fail**. Kill rate: 100% (above the ≥80% expectation).

**Per-drawer audit table:**

| Drawer axis | Stops | Identity-payload? | Action-payload? | Verdict | Content disposition |
|-------------|-------|-------------------|------------------|---------|---------------------|
| `stop-{1..6}-personal` | 6 | No (generic "personal reflection" prompts) | No (reflection, not next step) | CUT | Relevant reflection content absorbed into §4.4 (where I might be wrong) if load-bearing, else cut |
| `stop-{1..6}-creative` | 6 | No (generic creative framing) | No | CUT | Creative-angle content (e.g., naming / voice / aesthetic) moves to §4.3 (What I'd do first) — specific, not branched |
| `stop-{1..6}-client` | 6 | No (generic client-work framing) | Sometimes (stop-5 client had first-week habit specifics) | CUT | Client-work specifics (e.g., bilingual-market SEO angle, family-business-naming) promoted to §5 inline + §4.3; pointer-linked to `/research/seo-and-discovery.html` + `/research/growth-opportunities.html` for deeper treatment |
| `stop-{1..6}-deeper` | 6 | No (generic "more depth" signal) | No | CUT | Truly deeper material migrates to `/research/*.html` sibling pages per D1; one-line pointer in §6; never as main-page drawer |

**Replacement map (where the cut content re-surfaces).** Slice 4 consumes this as a pre-locked content inventory — no re-audit at build time:
- **Peer-cluster (the biggest identity-payload content in current drawers)** → promoted to §1 names-only teaser (D5) + full treatment in §4.1 + dossier on `/research/market-clusters.html` (Slice 5).
- **Bilingual-market / SEO angle** (currently buried in Stop-5 client drawer) → inline callout in §5 (first-week practice) + full treatment on `/research/seo-and-discovery.html`.
- **Family-business / attribution-naming angle** (currently Stop-3 creative drawer) → inline in §4.3 (What I'd do first).
- **Ceranna-segment moves** (currently scattered across stops 3–5 client drawers) → §4.1 (Where the market actually is) consumes.
- **Jeff Su habit specifics** (currently Stop-1 creative drawer) → §5 inline (first-week practice — "the one habit").
- **Generic reflection prompts** (Personal axis, all stops) → cut entirely; §4.4 "Where I might be wrong" does the reflective work at section level, not per-stop.

**Trade-off.** Risk: pre-locking drawer disposition in Slice 2 removes Slice 4's flexibility to re-audit when writing. Mitigation: the 4 axes are generic by inspection; Slice 4 build still owns the *wording* of how the replacement content surfaces inline — Slice 2 only locks the *disposition* (cut vs promote-inline) per axis. Recovery path if Jarda flags a cut post-ship: add back as inline callout (not as drawer), per standing D10 rule.

### D11 — Wireframes (inline HTML sketches)

Wireframes are committed as code blocks inside this blueprint, not as standalone `.html` files (per governance: no files written under `docs/design/2026-04-24-reshape/*` in this shaping session). Slice 4 (main build) extracts the skeleton; Slice 5 extracts the research page.

**Wireframe A — Main page (`/index.html` skeleton):**

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>For Jarda — AI + cowork refresher</title>
  <link rel="stylesheet" href="styles/shared.css">
</head>
<body class="main-brief">
  <header class="site-header">
    <div class="progress-line" aria-hidden="true"></div>
    <p class="last-updated">Last updated 2026-04-XX</p>
  </header>

  <main>
    <!-- §1 Opening (teaser-forward per D2) -->
    <section id="opening" aria-labelledby="opening-h">
      <h1 id="opening-h">For Jarda</h1>
      <div class="letter-body">
        <!-- 90s contract copy (D5) -->
        <!-- ~95w intro copy (D7) -->
        <!-- Peer-cluster names-only teaser: Ceranna · Avvagraphy · 2 Brides · Honest Guide · Paul Zizka -->
      </div>
    </section>

    <!-- §2 AI right now (Jeff Su + Jack Roberts — learning / memory-trigger) -->
    <section id="ai-now" aria-labelledby="ai-now-h">
      <h2 id="ai-now-h">AI right now — what Jeff &amp; Jack covered</h2>
      <article class="video-companion learning">
        <button type="button" class="yt-facade" data-youtube="z9rdrNrkvDY" aria-label="Play Jeff Su video">
          <img class="yt-facade-thumb" alt="">
          <span class="yt-facade-play" aria-hidden="true"></span>
          <span class="yt-facade-ts" aria-hidden="true"></span>
        </button>
        <div class="companion-text"><!-- Jeff Su ~150w memory-trigger --></div>
      </article>
      <article class="video-companion learning">
        <button type="button" class="yt-facade" data-youtube="cNf7uVff11Y" aria-label="Play Jack Roberts video">
          <img class="yt-facade-thumb" alt="">
          <span class="yt-facade-play" aria-hidden="true"></span>
          <span class="yt-facade-ts" aria-hidden="true"></span>
        </button>
        <div class="companion-text"><!-- Jack Roberts ~150w memory-trigger --></div>
      </article>
    </section>

    <!-- §3 Cowork world right now (Jesse Genet ×2 — interview / stand-alone) -->
    <section id="cowork-now" aria-labelledby="cowork-now-h">
      <h2 id="cowork-now-h">What people are actually building — Jesse Genet</h2>
      <article class="video-companion interview">
        <button type="button" class="yt-facade" data-youtube="yiJOTCRVWjc" aria-label="Play Jesse Genet a16z video">
          <img class="yt-facade-thumb" alt="">
          <span class="yt-facade-play" aria-hidden="true"></span>
          <span class="yt-facade-ts" aria-hidden="true"></span>
        </button>
        <div class="companion-text"><!-- Jesse a16z ~290w stand-alone + 2-3 quotes --></div>
      </article>
      <article class="video-companion interview">
        <button type="button" class="yt-facade" data-youtube="aFQskhdR3RQ" aria-label="Play Jesse Genet Cognitive Revolution video">
          <img class="yt-facade-thumb" alt="">
          <span class="yt-facade-play" aria-hidden="true"></span>
          <span class="yt-facade-ts" aria-hidden="true"></span>
        </button>
        <div class="companion-text"><!-- Jesse Cognitive Revolution ~295w stand-alone + 2-3 quotes --></div>
      </article>
    </section>

    <!-- §4 The brief (exec-summary with humility top + end per D9) -->
    <section id="the-brief" aria-labelledby="brief-h">
      <h2 id="brief-h">The brief I promised</h2>
      <div class="brief-handoff"><!-- ~110w D7 handoff copy carrying humility clause A --></div>
      <article id="brief-market"><h3>Where the market actually is</h3><!-- ~250w --></article>
      <article id="brief-moving"><h3>What's moving</h3><!-- ~200w --></article>
      <article id="brief-first-move"><h3>What I'd do first</h3><!-- ~250w --></article>
      <article id="brief-wrong">
        <h3>Where I might be wrong</h3>
        <!-- ~150w including humility clause B (D9 placement B) -->
      </article>
    </section>

    <!-- §5 First-week practice (inline — no drawers per D10) -->
    <section id="first-week" aria-labelledby="first-week-h">
      <h2 id="first-week-h">If it were me, first week</h2>
      <!-- ~250-350w; one habit, one setup, one project; any surviving go-deeper branches surface here INLINE as callouts, not drawers -->
    </section>

    <!-- §6 Deeper research (pointers to sibling /research/*.html pages) -->
    <section id="deeper" aria-labelledby="deeper-h">
      <h2 id="deeper-h">Deeper research — the folder I said was at the end</h2>
      <ul class="research-pointers">
        <li><a href="research/market-clusters.html">Market &amp; peer-cluster map</a> — the full breakdown behind the five names in §1</li>
        <li><a href="research/ten-year-picture.html">Ten-year picture</a> — long-range scenarios, Paul Zizka compounding analysis</li>
        <li><a href="research/seo-and-discovery.html">SEO + discovery</a> — bilingual-market angles, one-year moves</li>
        <li><a href="research/growth-opportunities.html">Growth opportunities</a> — Ceranna-shaped segment moves</li>
      </ul>
    </section>
  </main>

  <footer class="site-footer">
    <p>Stuck anywhere? Just ping me on WhatsApp — you know where to find me.</p>
    <!-- Footer fix per line-by-line synthesis hook #7: swap "reply to the email" → WhatsApp -->
  </footer>
</body>
</html>
```

**Wireframe B — Representative research page (`/research/market-clusters.html` skeleton, dossier aesthetic per C4):**

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Market &amp; peer-cluster map — research notes</title>
  <link rel="stylesheet" href="../styles/shared.css">
</head>
<body class="research-dossier"><!-- body class triggers dossier tint/typography per D12 -->
  <header class="research-header">
    <p class="dossier-humility">
      Surface-level scan. Written by Mark, desk-research not field-research — where I'm guessing vs. where I have evidence is flagged per block.
    </p>
    <h1>Market &amp; peer-cluster map</h1>
    <p class="back-link"><a href="../index.html">← back to the brief</a></p>
  </header>

  <main>
    <!-- Codex C4-proposed structure: Observed → Inferred → What-it-may-mean → First-experiment -->
    <article class="research-block">
      <h2>Ceranna</h2>
      <section class="observed"><h3>Observed</h3><!-- concrete facts --></section>
      <section class="inferred"><h3>Inferred</h3><!-- reading between the lines --></section>
      <section class="may-mean"><h3>What it may mean for Jarda</h3><!-- application --></section>
      <section class="experiment"><h3>First low-risk experiment</h3><!-- concrete action --></section>
    </article>

    <!-- Four more blocks: Avvagraphy / 2 Brides / Honest Guide / Paul Zizka — same structure -->
  </main>

  <footer class="research-footer">
    <p>Questions about any of this? WhatsApp.</p>
  </footer>
</body>
</html>
```

Both wireframes are structural only — no styling decisions beyond class names (styles come from shared.css in Slice 3). Body-class `.research-dossier` is the D12 trigger for the visible wrapper change.

### D12 — shared.css extraction plan (token inventory + file structure)

**File layout (Slice 3 creates; Slice 2 just inventories):**
```
jarda-ai-start/
├── index.html                    # main page (Slice 4 build)
├── styles/
│   └── shared.css                # Slice 3 extract target
└── research/
    ├── market-clusters.html      # Slice 5 build target
    ├── ten-year-picture.html     # Slice 5 build target
    ├── seo-and-discovery.html    # Slice 5 build target
    └── growth-opportunities.html # Slice 5 build target
```

**Token inventory** (Slice 3 implements via CSS custom properties on `:root` + body-class override for `.research-dossier`):

| Token group | Tokens | Notes |
|-------------|--------|-------|
| Colors | `--bg`, `--bg-dossier`, `--text`, `--text-muted`, `--accent`, `--link`, `--rule` | `.research-dossier` overrides `--bg` only |
| Typography scale | `--size-body`, `--size-h1`, `--size-h2`, `--size-h3`, `--size-small`, `--leading-body`, `--leading-tight` | Same scale across main + dossier; font-family may differ |
| Font families | `--font-body`, `--font-heading`, `--font-mono` | `.research-dossier` may override `--font-body` to a serif for "dossier" feel |
| Spacing | `--space-xs`, `--space-sm`, `--space-md`, `--space-lg`, `--space-xl` | 4-based scale (e.g., 4 / 8 / 16 / 24 / 48) |
| Breakpoints | `--bp-tablet`, `--bp-desktop` | Used via `@media` with custom property fallback pattern |
| Video facade | `.yt-facade` + `.yt-facade-thumb` + `.yt-facade-play` + `.yt-facade-ts` aspect ratio + hover state; `activateFacade(facade, startOverride)` JS hook + iframe-on-click preserved per synthesis D3 + existing [`index.html:1129`](../../../../index.html) pattern | **No change to markup or JS behavior** — wireframe A uses the current class names verbatim |

**Extraction order** (Slice 3 execution plan, confirmed but not implemented here):
1. Audit current `index.html` `<style>` block; extract reset + base typography first
2. Extract token definitions to `:root` + `.research-dossier` overrides
3. Extract component styles (video facade, callouts, progress line)
4. Extract section-level styles (`.main-brief main > section`, `.research-dossier .research-block`)
5. Delete `<style>` block from `index.html`; add `<link rel="stylesheet" href="styles/shared.css">`
6. Verify main page renders identically (pixel-diff pre/post extraction is Slice 3 acceptance criterion, not Slice 2's)

**Risk.** Dossier aesthetic shift (`.research-dossier` body class) may require tokens not yet in the inventory — e.g., `--bg-dossier-panel` if the block-level evidence labels get their own tint. Mitigation: inventory is a Slice 3 deliverable; Slice 2 documents the start-of-inventory set above, Slice 3 can extend without re-shaping.

**Existing selector preservation.** Slice 3 extraction must preserve the current `.research-*` class selectors from [`index.html`](../../../../index.html) — specifically the `.research-block` pattern that wraps each dossier section (per [line-by-line-ux-review.md:35](../../../research/2026-04-24-reshape-research/line-by-line-ux-review.md)). The dossier aesthetic ADDS four new selectors for evidence labeling (`.observed / .inferred / .may-mean / .experiment` — per wireframe B), but does not rename or remove any existing `.research-*` selectors; Slice 3's extraction is move-not-rewrite for these.

## Measurement Design

**1. What does this subsystem do, and who consumes its output?**
The artifact is a one-reader personal brief. Sole consumer: Jarda. Secondary: any other reader who overhears (architectural goal per Spike C: intimacy-with-second-audience-tolerance). There is no analytics pipeline, no A/B test, no funnel metric.

**2. How will we know this change made it better?**
Qualitative acceptance: Jarda can skim the shipped site in ~20 minutes and leave with the three deliverables named in the 90s contract (five peer names / one first-week habit / one-sentence brief). Binary: does he reach §4 and know where he sits in the market, or does he bounce before §2 ends? If he bounces, the reshape failed.

Pre-ship guardrails that approximate this qualitatively:
- Red-flag grep returns zero on all blueprint-drafted copy (verification command below; covered by AC).
- Opening-90s contract names Jarda in the first sentence (mechanical; covered by AC).
- Peer-cluster names appear above the first video embed (structural; covered by AC wireframe check).
- Humility clause appears exactly twice in §4 context — not once, not three times (D9 placement rule).

**3. What could get worse?**
- Single-page length fatigue: ~2000w main page. Mitigation: opening-90s contract + exec-summary brief both scannable; Go-Deeper audit cuts ornamental load.
- Dossier aesthetic may feel too-different from main page (C4 fix overshoots). Mitigation: body-class trigger shares token scale with main, only overrides `--bg` + optionally `--font-body`; not a parallel design system.
- Teaser-forward ordering may surprise an "academic-shaped" reader who expects intro → body → conclusion. Accept the surprise — Jarda is not an academic-shaped reader (Slice 1 memory-archaeology).

**Applicability.** N/A — qualitative first. An L-ticket docs/UX slice with N=1 consumer has no natural metric that isn't fake; mechanical AC + red-flag grep + wireframe checks approximate the qualitative goal without forcing a proxy.

## Acceptance Criteria

- [ ] PRD structure follows `/shaping` skill template: YAML frontmatter + Problem + Verified Assumptions + Shape Decision + Measurement Design + Acceptance Criteria + Slices + No-Gos + Verification Commands
- [ ] All 12 decisions (D1–D12) have explicit recommendation + reasoning + trade-off
- [ ] Opening-90s contract copy drafted inline (~175w, red-flag-grep clean); names Jarda in first sentence; closes with WhatsApp anchor
- [ ] Three "sounds like / doesn't sound like" sample pairs included verbatim from voice-audit.md (~50w each)
- [ ] At least one pair's "doesn't sound like" counter-sample absorbs a DHH-performed aphorism from synthesis C3 hit-list (Pair 3 absorbs "Specificity beats breadth" + "Trust compounds slowly")
- [ ] IA blueprint includes ~95w §1 intro copy + ~110w §4 handoff copy drafted inline
- [ ] §4 exec-summary brief outline has 4 sub-sections with word budgets totaling ~850w
- [ ] Humility clause appears at exactly TWO placements (top of §4 inside D7 handoff copy; end of §4 inside 4.4 body) with distinct verbs (active / procedural)
- [ ] Go-Deeper audit criterion upgraded to N=1 "would Jarda click this?" test with ≥80% expected kill rate documented
- [ ] Wireframe A (main page HTML skeleton) present inline as a code block, covers §1–§6
- [ ] Wireframe B (one representative research page, market-clusters.html) present inline as a code block with dossier aesthetic body class + evidence-label block structure
- [ ] shared.css token inventory documented (colors / typography / spacing / breakpoints / video facade)
- [ ] Footer copy swaps "reply to the email" → WhatsApp anchor (line-by-line synthesis hook #7)
- [ ] Red-flag grep on drafted copy (blockquote-scoped `^> `) returns zero matches for `opinionated|convention|as we say|turns out|the truth is|in our view` — denylist tokens in D4 voice guidance and meta-documentation are deliberately listed and are not in scope
- [ ] Codex CLI R1 + R2 review transcripts summarized in Appendix (decision history)
- [ ] Preflight aggregator exits 0 against this PRD

## Slices (this PRD's own execution)

### Slice 2 — single sub-slice (THIS DOCUMENT) [downhill]

**Demo.** `cat jarda-ai-start/docs/plans/prds/2026-04-24-reshape/slice-2-blueprint.md` prints a complete contract; preflight exits 0; user signs off.
**Files.** `jarda-ai-start/docs/plans/prds/2026-04-24-reshape/slice-2-blueprint.md`
**Steps.**
1. Lock D1–D12 with reasoning (done in Shape Decision above)
2. Draft opening-90s + §1 intro + §4 handoff copy inline (done in D5 + D7)
3. Import 3 sample pairs from voice-audit.md verbatim (done in D4)
4. Commit main-page + research-page wireframes inline (done in D11)
5. Document shared.css token inventory (done in D12)
6. Dispatch Codex CLI R1 (one focused question)
7. Fold R1 findings with smallest-diff discipline
8. Dispatch Codex CLI R2 (fold-verification, three-part question)
9. Run preflight aggregator; fix any stale rows
10. HARD STOP — present contract for user sign-off

**Tests.** Verification Commands section below.
**Depends on.** Slice 1 (shipped 2026-04-23).

## Downstream slice dependency map

This PRD unlocks Slices 3–7. Each is a separate per-slice-PRD shaping cycle when its turn comes; listed here for dependency tracking only.

| Slice | Consumes | Blocked until |
|-------|----------|---------------|
| Slice 3 — `shared.css` extraction | D11 wireframes + D12 token inventory | This PRD approved |
| Slice 4 — main-page build (`/index.html`) | D2 ordering + D3 vocabulary + D4 voice + D5 opening + D6 video titles + D7 IA + D8 brief outline + D9 humility placements + D10 Go-Deeper audit + D11 wireframe A | Slice 3 + this PRD approved |
| Slice 5 — research pages (4 × `/research/*.html`) | D1 structure + D11 wireframe B + D12 dossier tokens | Slice 3 + this PRD approved |
| Slice 6 — proofread pass | D4 voice + D9 humility + all red-flag grep rules | Slices 4+5 shipped |
| Slice 7 — ship (git init + GitHub Pages + Jarda handoff) | All above | Slice 6 signed off |

## Existing Patterns

- **Video facade pattern** — current `index.html` `.yt-facade` + iframe-on-click. Keep verbatim per synthesis D2/D3 resolution (no reviewer argued facade itself is broken). Re-home into shared.css via D12.
- **Progress line (thin) + last-updated stamp** — Gemini C1 recommendation absorbed; replaces current `Stop N of 6 · Block N of 3` chrome killed in D3.

## What This Replaces

- **`Stop N of 6 · Block N of 3` counter chrome** — [`jarda-ai-start/index.html`](../../../../index.html) (8 occurrences per VA row 7). E-learning identity signal; killed per D3 + C1 convergence.
- **24 `branch-drawer` entries (6 stops × 4 branches: Personal / Creative / Client / Deeper)** — [`jarda-ai-start/index.html:1538`](../../../../index.html) (pattern repeats at stops 2–6; 12 `Go deeper` label occurrences). All 24 fail the D10 N=1 test (generic audience axis, not Jarda-identity). 100% cut; content disposition locked in D10 replacement map.
- **"Reply to the email I sent you" footer copy** — current footer. Swapped to WhatsApp per synthesis hook #7.
- **Research section as visually-continuous "more content"** — current layout. Replaced by sibling `/research/*.html` pages with dossier aesthetic (body-class `.research-dossier`) per D1 + C4.

## No-Gos

- **No build work in this session.** No files written under `jarda-ai-start/docs/design/2026-04-24-reshape/*`. No HTML committed to `jarda-ai-start/*.html`. No `styles/shared.css` extracted. Slices 3–7 own the build.
- **No pre-shaping Slices 3–7.** Each gets its own `/shaping` cycle when its turn comes (per-slice-PRD pivot per umbrella plan decision 2026-04-23).
- **No re-litigating Slice 1 research findings.** Corrections → bench as follow-up items; not folded into this Slice 2 contract.
- **No `/practical/` sibling page.** Practical guidance lives inline in §5 per D1. (If Slice 4 build surfaces evidence that §5 inline gets long, shape a separate slice; don't drive-by-add.)
- **No voice re-drafting of the 3 sample pairs.** Pairs 1/2/3 are locked verbatim from voice-audit.md; any drift becomes a Slice 6 proofread finding, not a Slice 2 call.
- **No `git init` in `jarda-ai-start/`.** Slice 7's call, not this session.
- **No inline skills / hooks / rules work.** Any gap surfaces via `mcp__ccd_session__spawn_task`; do not edit `~/.claude/` files from this session.
- **No R3 Codex round.** Round cap is 2 per shape-up.md. R3 requires named directional contradiction per shape-up.md §Cross-Model Review — not expected here.

## Verification Commands

Run from `/Users/profile_1/Coding/jarda/`:

1. `test -f jarda-ai-start/docs/plans/prds/2026-04-24-reshape/slice-2-blueprint.md` — file exists and non-empty
2. `test -s jarda-ai-start/docs/plans/prds/2026-04-24-reshape/slice-2-blueprint.md` — non-empty
3. `bash ~/Coding/Agentic_Workflow_Setup/scripts/preflight-aggregator.sh jarda-ai-start/docs/plans/prds/2026-04-24-reshape/slice-2-blueprint.md` — exits 0 (stale-row + high-stakes-path + novel-path checks clean)
4. `! rg -n '^> .*\b(opinionated|convention|as we say|turns out|the truth is|in our view)\b' jarda-ai-start/docs/plans/prds/2026-04-24-reshape/slice-2-blueprint.md` — red-flag grep on blockquote-scoped drafted copy returns zero (denylist tokens in D4 voice guidance + meta-documentation are deliberate and not in scope)
5. `rg -q "^### D1 " jarda-ai-start/docs/plans/prds/2026-04-24-reshape/slice-2-blueprint.md && rg -q "^### D12 " jarda-ai-start/docs/plans/prds/2026-04-24-reshape/slice-2-blueprint.md` — D1 + D12 both present (brackets for D2–D11 verified by similar pattern in preflight run output)
6. `rg -q "Hi Jarda," jarda-ai-start/docs/plans/prds/2026-04-24-reshape/slice-2-blueprint.md` — opening contract drafted (names Jarda)
7. `rg -q "WhatsApp" jarda-ai-start/docs/plans/prds/2026-04-24-reshape/slice-2-blueprint.md` — footer + humility anchor references present

## Appendix — Codex R1/R2 review summary

Populated after R1 + R2 rounds complete. Entries include: round, dispatch question, verdict, findings list, fold action per finding, and any deliberate no-folds with reasoning.

### Codex R1 — Plan Review (2026-04-23)

**Dispatch question.** *"What is the biggest way this plan fails to deliver what was promised? What assumption is most likely wrong?"*

**Codex verdict.** Confidence: high. 5 Blockers · 3 Gaps · 3 Risks · 4 Proposed Alternatives.

**Headline.** *"The biggest way this plan fails the promise is straightforward: it says the peer-cluster identity payload moves into the opening 90 seconds, but the actual drafted opening still withholds that payload."*

**Findings + fold actions:**

| # | Codex finding | Severity | Fold action |
|---|---------------|----------|-------------|
| B1 | VA row 8 `Verify` cell uses `rg -q "go-deeper"` — current site has no `go-deeper` class; actual markup is `branch-drawer` + `Go deeper` label. Preflight would report verified-against-nonexistent-string. | Risk 4 | Rewrote VA row 8 claim + Source + Verify cell + Verified At to match `branch-drawer` class + `Go deeper` label (verified by grep: 24 + 12 occurrences). |
| B2 | Red-flag grep in AC L393 + Verify command L460 runs against the whole blueprint, which itself documents the denylist tokens (D4 L71, D5 L105) — check cannot pass as written. | Risk 5 | Scoped grep to blockquote-only lines (`^> ` prefix). Drafted copy uses blockquotes; denylist documentation is inline paragraph text. Pre-verified: zero matches on current blueprint. Updated AC, Verify command, D5/D7 notes. |
| B3 | D2 promises peer-cluster names move into opening 90s (teaser-forward mode-switch). D5 draft withholds the names themselves ("the names of five photographers… mapped below"). Central failure against the stated promise. | Risk 5 | Rewrote D5 opening: five names inline (**Ceranna, Avvagraphy, 2 Brides, Honest Guide, Paul Zizka**), mode-switch sentence ("if you want the brief first, jump straight to §4"), video skim guidance ("Jeff Su and Jack Roberts mostly refresher — skim or skip. Jesse Genet new, I'd read those"). Word count adjusted 140w → 175w. D7 §1 row updated. |
| B4 | D10 defers survivor enumeration to Slice 4 despite Slice 2 being the Blueprint contract. Leaves 24-drawer triage un-locked. | Risk 4 | Replaced deferred text with full 24-drawer audit table (6 stops × 4 axes; all generic — all cut). Added replacement map locking where each cut content type re-surfaces (§1 teaser / §4.1 / §4.3 / §5 / research-page pointers). Slice 4 consumes as pre-locked inventory. |
| B5 | Wireframe A uses `<div class="video-facade">` — actual site pattern at [index.html:1129,1494](../../../../index.html) is `<button class="yt-facade">` + `.yt-facade-thumb` / `.yt-facade-play` / `.yt-facade-ts` + `activateFacade()` JS hook. Slice 4 reading wireframe verbatim would break the pattern. | Risk 4 | Rewrote 4 facade blocks in wireframe A using exact `yt-facade` button markup; updated D12 facade token row to list the 4 class names + JS hook name + "no change to markup" note. |
| G2 | `.research-dossier` body class change to `/research/*.html` not fully reconciled with existing `.research-*` selectors in current `index.html`. | Gap | Added D12 "Existing selector preservation" paragraph: Slice 3 must preserve `.research-block` etc. move-not-rewrite; dossier ADDS `.observed/.inferred/.may-mean/.experiment` (never renames). |
| G3 | D8 4.2 says "Slice 4 picks which trend" — leaves the thesis un-anchored to peer-cluster evidence in 4.1; D8 sub-section order not locked despite 4.4 needing to close the section. | Gap | Reframed 4.2 as copywriting constraint: thesis must cite ≥2 peer names from 4.1. Locked sub-section order 4.1→4.2→4.3→4.4 explicitly; added rationale re humility placement B needing section close. |
| G1 (Codex) | "Dossier tokens (D12) not yet inventoried." | Gap | Documented: inventory is Slice 3 deliverable; Slice 2 locks start-of-inventory set above + extension policy ("Slice 3 can extend without re-shaping"). Trade-off accepted; not expanded into Slice 2. |
| R1–R3 (Codex) | 3 risks around reader-length fatigue, Slice 4 build surprise, dossier scope. | Risk | No direct fold. Trade-off already documented under the relevant decisions (D1 mitigation, D10 recovery path, D12 risk paragraph). |

**Proposed alternatives offered by Codex:** (a) merge D5 + §1 intro into one block [rejected — D7 distinguishes contract from intro copy for Slice 4 consumption]; (b) add a reader-length budget AC [partially folded — D1 mitigation already names the 20-minute skim target]; (c) split D10 into "axes audit" + "replacement map" [folded — D10 now contains both]; (d) promote humility clause to §1 [rejected — D9 rationale stands: the two placements do different jobs; §1 has its own mode-switch sentence which absorbs the "framing" role].

**Deliberate no-folds (with reasoning):** R1–R3 risks are accepted trade-offs, not blockers; Codex confidence=high on the B1–B5 blocker class. No regression-risk identified at fold time; R2 will verify.

### Codex R2 (fold-verification)

**Dispatch:** R2 = fold-verification pass per `rules/shape-up.md` round cap 2 + LEARNED.md 2026-04-18 (single-reviewer fold verification, distinct from council debate). Three-part question: (a) are R1 findings addressed? (b) any NEW regressions introduced by the folds? (c) any new cross-cutting concerns? Worktree access enabled; `model_reasoning_effort=high`; timeout 360s; exit code 0.

**Part A — Per-finding status (all 8 ADDRESSED)**

| # | Status | Justification |
|---|--------|---------------|
| B1 | ADDRESSED | VA row 8 verifies real site pattern (`class="branch-drawer"` + `Go deeper`) vs nonexistent `go-deeper`. |
| B2 | ADDRESSED | Denylist grep scoped to `^> ` blockquotes; no longer self-fails on D4/D5 meta-documentation; passes on current file. |
| B3 | ADDRESSED | D5 now names peer cluster inline (Ceranna, Avvagraphy, 2 Brides, Honest Guide, Paul Zizka) + §4 jump sentence + skim guidance. |
| B4 | ADDRESSED | D10 contains full 24-drawer audit + locked replacement map; Slice 4 consumes decided inventory, no re-triage. |
| B5 | ADDRESSED | Wireframe A uses live `.yt-facade` button pattern (`.yt-facade-thumb` / `.yt-facade-play` / `.yt-facade-ts`); D12 preserves `activateFacade(...)`. |
| G1 | ADDRESSED | D12 token inventory by group + extension policy — closes "not inventoried" gap. |
| G2 | ADDRESSED | D12 preserves `.research-*` selectors; dossier adds `.observed/.inferred/.may-mean/.experiment` only. |
| G3 | ADDRESSED | D8 anchors 4.2 to 4.1 evidence (≥2 peer names); locks 4.1→4.2→4.3→4.4 order. |

**Part B — Regressions introduced by folds**

1. **Word-budget drift (doc-hygiene only, fixed post-R2):** L89 and L419 still said `~140w` after B3 fold pushed draft to ~175–177w. Folded: L89 D5 header `~140w` → `~175w`; L419 AC bullet `~140w` → `~175w`. No content change; internal contradiction resolved.

**Part C — New cross-cutting concerns**

1. **Preflight exit code in read-only sandbox:** R2 Codex sandbox reported preflight exit 0 alongside temp-file failures + 0 VA rows / 0 novel paths checked. "Preflight green" is not strong evidence until re-run in writable environment. Owner: session-final preflight step before user approval (not R2 blocker).

**Verdict:** Confidence = high. No shape-changing contradiction that would justify R3 per `rules/shape-up.md` directional-contradiction test. R1 structural issues closed; Slice 4 now has contract-level inputs (opening carries identity payload / drawer disposition locked / research-page dossier relationship specified / facade markup matches live site). Codex R2 full output at `/tmp/codex-r2-2KpdX8/out.md`.
