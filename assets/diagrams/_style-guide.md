# Excalidraw Style Guide — jarda-ai-start v2

All 6 diagrams in v2 follow these rules for visual consistency. The aesthetic is "hand-drawn, intentionally anti-AI-slop" — Excalidraw's default rough roughness, not pixel-perfect design-tool polish.

## Rules

- **Line weight**: 2px strokes, consistently. No thin hairlines, no thick accents.
- **Ink color**: `#222` for primary strokes + labels. `#a84b2b` (accent) for focal callouts only — one per diagram maximum.
- **Label font**: Inter, 11–13px. No fancy serif, no emoji.
- **Fill**: White or `#fafaf7` (bg-inset). No gradient fills, no solid bright colors.
- **Annotations**: 2–5 words max per label. "Project memory" not "The project-level memory storage system."
- **Hand-drawn wobble**: use Excalidraw's default "sloppy" roughness (not "architect" — too clean, not "artist" — too wobbly).

## Per-diagram specifics

1. **stop-1-positioning** — four boxes in a row: ChatGPT | Cowork | Code | Codex. Annotations: "single-turn", "with memory + files (recommended)", "developer-grade", "CLI-based". Accent color on "Cowork" box.
2. **stop-2-project-anatomy** — one outer box labeled "Project", three inner boxes: Instructions · Files · Memory. Accent on "Files" (the new thing a beginner hasn't seen).
3. **stop-3-memory-scopes** — nested boxes: System (largest) > Project > Chat (smallest). Labels on each. Accent on "Project" (the recommended scope).
4. **stop-4-connector-scope** — concentric circles: "what Cowork sees" (inner), "what it can write" (middle), "what it cannot touch" (outer boundary). Example labels at each level.
5. **stop-5-workflow-anatomy** — horizontal arrow flow: Input → Transform → Check → Output. Labels describe a generic use case.
6. **stop-6-habit-loop** — cyclic arrow: Trigger → Action → Reflect → Refine → (back to Trigger). Small example text per node.

## v2a placeholder SVGs (this task + Slice 2)

Because this codebase is built by subagents without Excalidraw-GUI access, Stop 1–3 SVGs ship as hand-styled SVG code that **mimics** Excalidraw's hand-drawn look:

- Use SVG `<path d="M... Q..." />` with deliberate small jitter on coordinates (±1–2px) to simulate wobbled strokes
- `stroke-linecap="round"` and `stroke-linejoin="round"`
- `stroke-width="2"` consistently
- Fills: none or `#fafaf7`
- Text in `font-family: 'Inter', system-ui, sans-serif; font-size: 12`

These are **placeholders for a real Excalidraw pass** after v2a ships. To refine: open `excalidraw-source/<name>.excalidraw` in Excalidraw, recreate, export SVG, overwrite.

## Export process (for real Excalidraw refinement later)

1. Open `excalidraw-source/<name>.excalidraw` in Excalidraw web app (no login)
2. If file is a stub, recreate from style-guide rules
3. Save as `.excalidraw` source (overwrite stub)
4. Export → SVG → overwrite `assets/diagrams/<name>.svg`
   - Embed font: NO (smaller file)
   - Background: transparent
5. Verify SVG ≤50KB
6. Commit both source and SVG
