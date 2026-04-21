# AI Start — placeholder onboarding

A single-page, self-paced primer for a non-technical creator adopting Claude Cowork and (eventually) Claude Code.

**This public repo is a PLACEHOLDER.** The real name, real URLs, and real referral codes never land here. The real version ships via DM.

The page uses "Jay Z" as the reader persona.

---

## What's in the repo

- `index.html` — the primer. A 6-stop spine + branches course, no dependencies, no backend, no analytics. Stops 1–3 populated in v2a; stops 4–6 placeholders for v2b.
- `assets/diagrams/` — 3 hand-styled SVG positioning diagrams (one per populated stop). Style rules in `_style-guide.md`.
- `excalidraw-source/` — `.excalidraw` source stubs. Real Excalidraw files land later via GUI pass.
- `.gitignore` — keeps contracts, research, verification artifacts, and private-customized variants out of Git.

### Deliberately NOT in the repo

- `docs/plans/` — gitignored. Contract + slice plans live here locally; they contain real details.
- `docs/research/` — gitignored. Loose research threads.
- Any private-name customized variant. The private appendix lives outside this repo, in the umbrella working directory.

---

## Lifecycle + takedown

This page is a one-off handoff artifact for one reader. Planned lifecycle:

1. Build + deploy v2a (stops 1–3 live)
2. Share URL with reader; 7-day verify window
3. Build v2b (stops 4–6 + completion state + public appendix) if engagement signal arrives
4. Take down: **either** reader confirms "I've got what I need," **or** 30 days from deploy, whichever first

Before takedown: capture to vault alongside other shipped projects (index.html, diagrams, lessons learned).

---

## Privacy

A denylist-based audit runs against every commit. Patterns include literal names, URL-encoded variants, Czech diacritics, hyphen-variants, and referral-URL regexes. The audit tool lives **outside this repo** — in the umbrella working directory — so the denylist itself never ships publicly.

**Real codes and real names NEVER go in Git.** Once pushed, they're in history forever. Rotate a leaked code; don't try to rewrite history on a repo that's been cloned.

---

## Known limitations (v2a)

- Stops 4–6 show "Coming in a few days" placeholders. v2b fills them after a verify signal.
- No completion state yet (stop 6 try-one → reveal); ships in v2b Slice 6.
- No public appendix yet (tool landscape + market map + "why these six stops"); ships in v2b Slice 7.
- Static HTML only. No cross-device progress sync — each browser has its own `localStorage`.
- No analytics. No way to observe engagement; the reader tells us directly or the signal is silence.
