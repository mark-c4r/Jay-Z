# AI Start — placeholder onboarding

A single-page, self-paced primer for a non-technical creator adopting Claude Cowork and (eventually) Claude Code.

**This public repo is a PLACEHOLDER.** The real name, real URLs, and real referral codes never land here. The real version ships via DM.

The page uses "Jay Z" as the reader persona.

---

## What's in the repo

- `index.html` — the primer. A 6-stop spine + branches course, no dependencies, no backend, no analytics. All 6 stops populated, with a completion state and a public-research appendix.
- `assets/diagrams/` — 6 hand-styled SVG positioning diagrams (one per stop). Style rules in `_style-guide.md`.
- `assets/hero-summit.jpg` — ridgeline photo used in the completion reveal.
- `excalidraw-source/` — `.excalidraw` source stubs. Real Excalidraw files land later via GUI pass.
- `.gitignore` — keeps contracts, research, verification artifacts, and private-customized variants out of Git.

### Deliberately NOT in the repo

- `docs/plans/` — gitignored. Contract + slice plans live here locally; they contain real details.
- `docs/research/` — gitignored. Loose research threads.
- Any private-name customized variant. The private appendix lives outside this repo, in the umbrella working directory.

---

## Lifecycle + takedown

This page is a one-off handoff artifact for one reader. Planned lifecycle:

1. Build + deploy (done — all 6 stops populated, completion state live, research appendix available).
2. Share URL with reader.
3. Take down: **either** reader confirms "I've got what I need," **or** 30 days from deploy, whichever comes first.

Before takedown: capture to vault alongside other shipped projects (index.html, diagrams, lessons learned).

---

## Privacy

A denylist-based audit runs against every commit. Patterns include literal names, URL-encoded variants, Czech diacritics, hyphen-variants, and referral-URL regexes. The audit tool lives **outside this repo** — in the umbrella working directory — so the denylist itself never ships publicly.

**Real codes and real names NEVER go in Git.** Once pushed, they're in history forever. Rotate a leaked code; don't try to rewrite history on a repo that's been cloned.

---

## Known limitations

- Static HTML only. No cross-device progress sync — each browser has its own `localStorage`.
- No analytics. No way to observe engagement; the reader tells us directly or the signal is silence.
- YouTube embeds use click-to-play facades with per-segment thumbnails. The first click bootstraps the iframe and autoplays the chosen segment. Safari Low Power Mode may suppress the autoplay — the YouTube play button in the iframe is a single-click fallback.
- The `.excalidraw` source files are placeholder stubs. Diagram authoring via the real Excalidraw GUI happens outside this repo.
