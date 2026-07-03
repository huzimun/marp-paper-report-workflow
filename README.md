# Marp Paper Report Workflow

[中文说明](README.zh-CN.md)

`marp-paper-report-workflow` is a Codex skill for paper-grounded Marp/Markdown academic presentation workflows. It helps turn a slide deck based on research papers into a versioned, auditable workflow: papers are collected, summarized in Chinese, checked against slide claims, used for figure extraction or annotation, compiled into Marp PDFs, and recorded in version logs.

## What To Prepare

Create a dedicated project folder for each deck. Put any available materials there:

- A Marp/Markdown slide deck, preferably `.marp.md` or `.md`.
- Paper PDFs, if you already have them.
- Paper titles, DOI links, arXiv IDs, publisher links, or citation lists.
- Meeting notes or slide-editing requirements.
- Specific approval instructions, such as pages to edit or facts to confirm.

You can start with only a slide deck and paper names. If Codex cannot download a paper from the publisher, it should ask for a local PDF or use a public repository only after verifying that title, authors, year, DOI, and version match.

## Recommended Project Structure

The skill creates or uses a project-local output structure like this:

```text
project-folder/
├── deck.marp.md
├── workflow_outputs/
│   ├── papers/
│   ├── figures/
│   ├── artifacts/
│   ├── versions/
│   ├── paper_manifest.md
│   ├── paper_summaries.md
│   ├── fact_check_report.md
│   └── version_log.md
```

Keep private files in the project folder. Do not upload private papers or decks to online editors unless you explicitly approve it.

## Typical Workflow

1. Create a dedicated project folder and place the slide deck and known materials in it.
2. Ask Codex to use `$marp-paper-report-workflow`.
3. Codex identifies the deck, referenced papers, placeholders, and missing evidence.
4. Codex downloads or organizes PDFs and verifies paper identity.
5. Codex writes `paper_manifest.md` and `paper_summaries.md`.
6. Codex checks key slide claims against source papers and records human-verifiable evidence.
7. Codex fills requested figures, crops or annotates paper images, redraws diagrams when appropriate, and keeps slide source notes consistent.
8. Codex compiles the Marp Markdown into PDF, checks representative pages visually, and records the iteration.
9. You review facts, layout, and final output before approval.

## Capabilities

- Build a paper manifest with title, authors, venue, year, DOI/arXiv, source link, local PDF, and verification status.
- Generate 150-300 Chinese character summaries for every paper so users can quickly understand long English PDFs.
- Trace slide claims back to paper excerpts, PDF pages, sections, figures, or tables.
- Extract, crop, annotate, or simplify paper figures while preserving source information.
- Use Marp-compatible HTML/CSS/SVG for conceptual diagrams.
- Compile versioned Marp Markdown to PDF.
- Maintain a version log with changed pages, commands, visual checks, approval status, and unresolved issues.

## Outputs

Typical deliverables include:

- Versioned Marp Markdown files.
- Versioned PDFs.
- `paper_manifest.md`
- `paper_summaries.md`
- `fact_check_report.md`
- `version_log.md`
- Figure assets used by the slides.

Standalone HTML is not a normal deliverable. Inline HTML/CSS/SVG may be used inside Marp Markdown for drawing.

## Versioning Rules

- Treat the original deck as the baseline.
- Do not overwrite approved versions.
- Create each new formal revision as `deck.workflow-vNN.marp.md` with a matching `deck.workflow-vNN.pdf`.
- Store formal history under `workflow_outputs/versions/`.
- Store temporary candidates and inspection files under `workflow_outputs/artifacts/`.
- Record every formal revision in `workflow_outputs/version_log.md`.

## Privacy And Safety

- Do not include personal paths, usernames, credentials, cookies, or private URLs in public records.
- Prefer relative project paths such as `workflow_outputs/papers/...`.
- Do not upload private PDFs or decks to online tools without explicit approval.
- If a paper is obtained from a non-publisher source, verify that it is the same paper before using it.

## Example Prompt

```text
Use $marp-paper-report-workflow to fact-check and revise this paper-based Marp presentation with versioned outputs. Generate Chinese summaries for all papers, fill only pages with figure placeholders, compile a PDF, and record the version log.
```

## License

MIT License. See `LICENSE`.
