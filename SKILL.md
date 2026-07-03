---
name: marp-paper-report-workflow
description: Automate paper-grounded Marp/Markdown slide workflows for academic presentations. Use when Codex needs to fact-check claims against papers, download or organize paper PDFs, extract and cite figures/tables, revise Marp slides, compile PDF previews, validate VS Code/Marp CLI/online editor paths, record human-verifiable evidence, and manage versioned iterations safely.
---

# Marp Paper Report Workflow

## Goal

Turn a paper-based Marp presentation into a verifiable, versioned, and mostly automated workflow: the user states needs and approves key results; Codex handles evidence tracing, page edits, figure generation or extraction, PDF preview, and iteration records.

## Core Rules

- Preserve user work. Never overwrite the source deck directly; create a versioned working copy and outputs.
- Edit only pages the user names or pages containing explicit placeholders such as `鍥捐〃鍗犱綅`, unless the user approves broader edits.
- Keep privacy out of reusable records. Do not hard-code personal names, local home paths, course folders, credentials, or private URLs in skill outputs.
- Prefer traceable evidence over polished prose. Every factual claim kept in the deck should be supported, corrected, labeled as inference, or marked unresolved.
- Treat PDF as the final preview/export artifact. Use inline HTML/CSS/SVG only as a Marp drawing method; keep standalone HTML only when needed for inspection or debugging.
- Keep the user role narrow: request requirements, ask for missing papers or factual approvals, and ask for final visual approval.

## Workflow

1. Create a versioned workspace:
   - Detect the source `.md`/`.marp.md`.
   - Create `workflow_outputs/` with `papers/`, `figures/`, `artifacts/`, and `versions/` or an equivalent project-local structure.
   - Copy the source deck to a timestamped or semver-style working file before editing.
   - Record each iteration in a change log with deck version, changed pages, reason, commands, and outputs.

2. Build the evidence base:
   - Identify referenced papers from the deck and meeting notes.
   - Download or use user-provided PDFs. If publisher download fails, use arXiv or another repository only after confirming title, authors, year, DOI, and version match.
   - Create a paper manifest with title, authors, venue, year, DOI/arXiv, source link, local filename, and verification status.
   - For detailed fields, read `references/fact-checking.md`.

3. Fact-check the deck:
   - Work page by page.
   - For each key claim, capture: slide page, slide text, source paper, original excerpt, exact location, conclusion, and action.
   - Classify each claim as supported, needs correction, inference/extension, or unresolved.
   - Provide a human verification path using local PDF filename, page/section/figure/table, and short original excerpt.

4. Revise figures and layout:
   - Use paper originals for empirical results and named figure placeholders.
   - Use cropped originals or simplified redraws only when the original is too dense, while preserving a source note.
   - When a placeholder asks for labels or annotations, produce an annotated figure rather than inserting the raw original unchanged.
   - Write figure explanations with a traceable opening such as `Author et al. Fig. 1:` or `Author et al. Table 1:`. Do not start with generic labels such as `璇诲浘锛歚.
   - Make every figure explanation stand alone: a reader should understand what the figure means from the image plus the explanation, without relying on presenter narration.
   - Use HTML/CSS/SVG inside Marp for concepts, mechanisms, and process diagrams.
   - Use generated bitmap images only for strongly visual/illustrative needs.
   - Put every source note on the slide bottom line in one consistent format:
     `鏉ユ簮锛欰uthor et al., Paper Title, Venue, Year, https://...`
   - For layout checks and page rules, read `references/marp-layout.md`.

5. Compile and inspect:
   - Prefer VS Code local Marp preview when available.
   - Always verify Marp CLI export when feasible: compile the working Markdown to PDF with local files enabled if images are embedded.
   - Verify the online editor path as a fallback workflow when requested or when portability is part of the task.
   - Inspect representative pages visually, including boundary margins, image readability, font consistency, and source footer placement.

6. Validate automation samples:
   - Run at least two or three representative pages through the full loop: user request, Codex edit, compile/preview, approval point, iteration, final result.
   - Include one paper-original figure page, one generated/HTML concept page, and one complex layout page when such pages exist.
   - Record exact slide page numbers, changed files, commands, outputs, approval points, and rework count.

7. Deliver:
   - Versioned working Marp Markdown.
   - Generated PDF.
   - Paper manifest.
   - Fact-check record with human-verifiable excerpts and locations.
   - Workflow validation record with page numbers.
   - Marp environment validation conclusion and fallback path.

## Version Management

Read `references/versioning-and-safety.md` before substantial edits, multi-round revisions, or any task involving privacy/security constraints.

## Useful References

- Read `references/fact-checking.md` when extracting claims, building a paper manifest, or preparing human verification materials.
- Read `references/marp-layout.md` when editing slides, generating figures, validating PDF output, or comparing VS Code/CLI/online Marp workflows.
- Read `references/versioning-and-safety.md` when setting up output folders, naming versions, recording iterations, or sanitizing deliverables.
