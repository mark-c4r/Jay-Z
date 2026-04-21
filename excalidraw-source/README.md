# Excalidraw sources

These `.excalidraw` files are **stubs** — minimal empty files that open cleanly in the Excalidraw web app. The shipping SVGs at `../assets/diagrams/*.svg` are hand-styled SVG code written during v2a build (subagents can't operate the Excalidraw GUI).

To refine a diagram:
1. Open the `.excalidraw` stub in [excalidraw.com](https://excalidraw.com)
2. Recreate the diagram from `../assets/diagrams/_style-guide.md` specs
3. Save over the `.excalidraw` stub (File → Save)
4. Export → SVG → overwrite `../assets/diagrams/<name>.svg`
5. Commit both
