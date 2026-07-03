# Marp Layout and Environment Reference

## Page Editing Rules

- Modify only pages named by the user or pages with explicit placeholders such as `图表占位`.
- Record the exact slide page number for every sample and every edit.
- Keep a visible margin on all sides after PDF export.
- Keep source notes in the bottom line, with consistent format:
  `来源：Author et al., Paper Title, Venue, Year, https://...`
- Avoid large text blocks beside tiny figures. Prioritize readable figures and concise interpretation.
- For original paper figures, make the figure large enough to read labels that matter to the slide purpose.
- Use compact Chinese figure explanations that explain what the figure demonstrates, not merely that it is complex.
- Start each figure explanation with the paper and exact figure/table number, for example `Steyvers et al. Fig. 1:`. Do not use generic openings such as `读图：`.
- Ensure each figure explanation satisfies four checks: it matches the slide `用途` and `截图建议`; it reflects the original paper figure/table title or caption; it fits the surrounding slide text; and it is independently understandable from the image plus explanation alone.
- Keep font sizes coordinated across title, body, figure note, and source footer.

## Figure Strategy

- Paper result or named placeholder: use the requested original figure/table/crop.
- If the screenshot suggestion requests Chinese labels or callouts, create an annotated version of the figure. Prefer GPT image editing when the environment supports passing the original image as input; otherwise use a reproducible local method such as SVG/HTML/Canvas overlays, and save the annotated asset under `figures/`. Do not obscure original figure content; place labels in margins, whitespace, or a separate legend band, and avoid arrows or boxes that cover data, text, or icons. Always inspect the exported PDF/PNG; if SVG text renders incorrectly or fonts are missing, rasterize the annotated figure to PNG.
- Dense original: crop the relevant region or redraw a simplified schematic, while citing the original figure/table.
- Concept/process/mechanism: draw with inline HTML/CSS/SVG inside Marp.
- Illustration-heavy need: generate a bitmap image, save it under `figures/`, and cite it as generated material if not paper evidence.

## Marp Export

Prefer a project-local command similar to:

```powershell
npx marp "path/to/deck.marp.md" -o "path/to/output.pdf" --html --allow-local-files
```

Use `--html` only to allow inline HTML in Marp rendering. The deliverable can still be Markdown plus PDF; do not retain standalone HTML unless needed for debugging.

## Environment Validation

Validate all requested editor paths when portability matters:

- VS Code path: open the working Markdown, preview Marp, edit, and export or compare with CLI output.
- Marp CLI path: install or call the CLI, export PDF, and record dependency or browser errors.
- Online editor path: import Markdown, preview, edit if practical, export if supported, and record differences from local output.

For each path, record startup cost, stability, preview accuracy, export quality, collaboration suitability, success conditions, and failure modes.
