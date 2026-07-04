# Marp Layout and Environment Reference

## Page Editing Rules

- Modify only pages named by the user or pages with explicit placeholders such as `图表占位`.
- Record the exact slide page number for every sample and every edit.
- Before editing a placeholder page, copy the original `图表占位`, `用途`, and `截图建议` into the working notes or version log and treat them as acceptance criteria.
- Keep a visible margin on all sides after PDF export.
- Keep source notes in the bottom line, with consistent format:
  `来源：Author et al., Paper Title, Venue, Year, https://...`
- Avoid large text blocks beside tiny figures. Prioritize readable figures and concise interpretation.
- For original paper figures or user-provided figure assets, make the figure large enough to read labels that matter to the slide purpose.
- Use compact Chinese figure explanations that explain what the figure demonstrates, not merely that it is complex.
- Start each figure explanation with the paper and exact figure/table number, for example `Steyvers et al. Fig. 1:`. Do not use generic openings such as `读图：`.
- Ensure each figure explanation satisfies four checks: it matches the slide `用途` and `截图建议`; it reflects the original paper figure/table title, caption, or visible content; it fits the surrounding slide text; and it is independently understandable from the image plus explanation alone.
- Keep font sizes coordinated across title, body, figure note, figure labels, and source footer.

## User-Provided Asset Layout

Use this checklist in Fast Figure Fill Mode.

- Treat the provided PNG/JPG/SVG/PDF crop as the selected asset. Do not re-extract the same figure from a paper PDF unless the asset is missing, unreadable, or clearly mismatched.
- Do not alter image pixels for labels, arrows, translations, or highlighting unless the user explicitly asks for raster annotation.
- Add labels, callouts, legends, or reading guides in Marp Markdown/HTML/CSS around the asset.
- Preserve the full provided image when the user supplies a complete figure/table or asks to use it as-is.
- Crop only when the slide requirement still calls for a crop and the user has not overridden that instruction.
- Keep the slide explanation short enough that the exported PDF retains bottom margin and source footer visibility.
- Prefer producing the PDF quickly for user inspection when the user asks to see the result before continuing.

## Figure Strategy

- User-provided figure/table asset: use it directly in Fast Figure Fill Mode.
- Paper result or named placeholder without a provided asset: use the requested original figure/table/crop in Full Paper Audit Mode.
- For paper figures and tables, keep a clean complete figure/table asset as the traceable source when Codex extracts it.
- If the user provides or requests the complete figure, insert the complete figure and satisfy labels/callouts in Marp around the image.
- Create slide-specific local crops only when the placeholder still requires a crop and the user has not overridden that requirement.
- If the screenshot suggestion requests Chinese labels or callouts, add them in Marp Markdown/HTML/CSS outside or around the image. Place labels in margins, whitespace, a separate legend band, or adjacent callout blocks, and avoid covering data, text, or icons.
- Always inspect the exported PDF/PNG; if Marp-rendered text breaks layout, adjust the Marp labels before rasterizing anything.
- For portrait figures, prefer a three-column layout when it fits: slide text plus longer explanation on the left, the complete figure in the center, and short callouts stacked vertically on the right.
- Dense original: crop the relevant region or redraw a simplified schematic, while citing the original figure/table.
- Concept/process/mechanism: draw with inline HTML/CSS/SVG inside Marp.
- Illustration-heavy need: generate a bitmap image, save it under `figures/`, and cite it as generated material if not paper evidence.

## Placeholder Acceptance Checklist

For each filled placeholder, verify all of the following before delivery:

- The slide page number matches the user request or an explicit placeholder.
- The inserted asset comes from the requested paper and figure/table number, is the user-provided asset for that placeholder, or the version log records the user-approved deviation.
- The asset satisfies the slide `用途`.
- The asset satisfies the `截图建议`, including crop scope and annotation requirements.
- The figure explanation starts with the paper and exact figure/table number and is independently understandable.
- The exported PDF/PNG has readable image details, no overlap, no clipped content, coordinated fonts, and a bottom-line source note.

## Marp Export

Prefer a project-local command similar to:

```powershell
npx marp "path/to/deck.marp.md" -o "path/to/output.pdf" --html --allow-local-files
```

Use `--html` only to allow inline HTML in Marp rendering. The deliverable can still be Markdown plus PDF; do not retain standalone HTML unless needed for debugging.

If direct PDF export fails but HTML export works, a project may use an already validated local fallback such as a browser/Edge/Puppeteer PDF print path. Record the fallback command and do not present standalone HTML as the final deliverable unless the user requested it.

## Environment Validation

Validate editor/export paths when portability matters or when a requested path has changed:

- VS Code path: open the working Markdown, preview Marp, edit, and export or compare with CLI output.
- Marp CLI path: install or call the CLI, export PDF, and record dependency or browser errors.
- Browser fallback path: export HTML with local files enabled, then print to PDF with the validated local browser engine.
- Online editor path: use only when requested or when local tooling is unavailable, and state the privacy risk before uploading private decks or papers.

For each path, record startup cost, stability, preview accuracy, export quality, collaboration suitability, success conditions, and failure modes.
