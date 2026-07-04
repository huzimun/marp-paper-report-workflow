# Marp Paper Report Workflow

[中文说明](README.zh-CN.md)

`marp-paper-report-workflow` is a Codex skill for paper-grounded Marp/Markdown academic presentation workflows. It supports two modes:

- **Fast Figure Fill Mode** for user-provided figure/table assets that only need to be placed into slides with concise explanations, source notes, PDF export, and visual checks.
- **Full Paper Audit Mode** for downloading or organizing papers, extracting figures, fact-checking slide claims, generating Chinese summaries, and maintaining full audit records.

The skill keeps slide work versioned, auditable, and scoped to the user's actual request.

## What To Prepare

Create a dedicated project folder for each deck. Put any available materials there:

- A Marp/Markdown slide deck, preferably `.marp.md` or `.md`.
- User-provided figure/table images or screenshots when you want a fast fill workflow.
- Paper PDFs, if full audit or figure extraction is needed.
- Paper titles, DOI links, arXiv IDs, publisher links, or citation lists.
- Meeting notes or slide-editing requirements.
- Specific approval instructions, such as pages to edit or facts to confirm.

You can start with only a slide deck and user-provided figure images. In that case Codex should use Fast Figure Fill Mode and avoid paper downloads unless the asset identity or explanation cannot be handled safely.

## Recommended Project Structure

The skill creates or uses a project-local output structure like this:

```text
project-folder/
├── deck.marp.md
└── workflow_outputs/
    ├── papers/
    ├── figures/
    ├── artifacts/
    ├── versions/
    ├── paper_manifest.md
    ├── paper_summaries.md
    ├── fact_check_report.md
    └── version_log.md
```

Fast mode may only update `figures/`, `artifacts/`, `versions/`, and `version_log.md`. Full mode may also update `papers/`, `paper_manifest.md`, `paper_summaries.md`, and `fact_check_report.md`.

Keep private files in the project folder. Do not upload private papers or decks to online editors unless you explicitly approve it.

## Fast Figure Fill Mode

Use this mode when you already provide the needed image/table assets and want Codex to fill specific slides quickly.

Typical workflow:

1. You provide page numbers and image/table files.
2. Codex reads the placeholders, `用途`, `截图建议`, and nearby teaching point.
3. Codex inserts the provided asset, writes a standalone Chinese explanation, and adds a consistent source footer.
4. Codex exports a PDF preview and visually checks the changed pages.
5. Codex records a compact version-log entry and pauses for your inspection when requested.

Fast mode does not normally download PDFs, extract figures, rebuild the paper manifest, generate all paper summaries, or fact-check the whole deck.

Example prompt:

```text
Use $marp-paper-report-workflow in Fast Figure Fill Mode. I have provided the images for pages 57, 66, and 67. Insert them, write suitable Chinese explanations based on the placeholders, export a PDF, and pause for review.
```

## Full Paper Audit Mode

Use this mode when you need paper-grounded evidence work.

Typical workflow:

1. Codex identifies the deck, referenced papers, placeholders, and missing evidence.
2. Codex downloads or organizes PDFs and verifies paper identity.
3. Codex writes `paper_manifest.md` and `paper_summaries.md`.
4. Codex checks key slide claims against source papers and records human-verifiable evidence.
5. Codex fills requested figures, crops or annotates paper images, redraws diagrams when appropriate, and keeps slide source notes consistent.
6. Codex compiles the Marp Markdown into PDF, checks representative pages visually, and records the iteration.
7. You review facts, layout, and final output before approval.

Example prompt:

```text
Use $marp-paper-report-workflow in Full Paper Audit Mode to fact-check this paper-based Marp presentation, download or organize the cited papers, extract missing figures, compile a PDF, and record the version log.
```

## Capabilities

- Choose between fast figure fill and full paper audit workflows.
- Preserve versioned Marp Markdown and PDF outputs.
- Fill named slide pages with user-provided assets and concise Chinese explanations.
- Build a paper manifest with title, authors, venue, year, DOI/arXiv, source link, local PDF, and verification status.
- Generate 150-300 Chinese character summaries for papers when full audit mode needs them.
- Trace slide claims back to paper excerpts, PDF pages, sections, figures, or tables.
- Extract, crop, annotate, or simplify paper figures while preserving source information.
- Use Marp-compatible HTML/CSS/SVG for conceptual diagrams.
- Maintain a version log with changed pages, commands, visual checks, approval status, and unresolved issues.

## Outputs

Fast mode deliverables usually include:

- Versioned Marp Markdown files.
- Versioned PDFs.
- Figure assets used by the slides.
- `version_log.md`.

Full mode may additionally include:

- `paper_manifest.md`.
- `paper_summaries.md`.
- `fact_check_report.md`.

Standalone HTML is not a normal deliverable. Inline HTML/CSS/SVG may be used inside Marp Markdown for drawing.

## Versioning Rules

- Treat the original deck as the baseline.
- Do not overwrite approved versions.
- Create each new formal revision as `deck.workflow-vNN.marp.md` with a matching `deck.workflow-vNN.pdf`.
- Store formal history under `workflow_outputs/versions/`.
- Store temporary candidates and inspection files under `workflow_outputs/artifacts/`.
- Record every formal revision in `workflow_outputs/version_log.md`.
- If a user asks to delete or redo a version, mark the old formal version as rejected, deprecated, or superseded in the log instead of silently removing the audit trail.

## Privacy And Safety

- Do not include personal paths, usernames, credentials, cookies, or private URLs in public records.
- Prefer relative project paths such as `workflow_outputs/papers/...`.
- Do not upload private PDFs or decks to online tools without explicit approval.
- If a paper is obtained from a non-publisher source, verify that it is the same paper before using it.

## License

MIT License. See `LICENSE`.
