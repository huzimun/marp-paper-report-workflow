---
name: marp-paper-report-workflow
description: Automate paper-grounded Marp/Markdown slide workflows for academic presentations, with a fast mode for user-provided figure assets and a full mode for paper auditing, extraction, citation, PDF preview, and versioned iteration records.
---

# Marp Paper Report Workflow

## Goal

Turn a paper-based Marp presentation into a verifiable, versioned, and appropriately scoped workflow. Codex should first choose the lightest mode that satisfies the user's current request, then handle only the required slide edits, evidence tracing, export checks, packaging, and records without overwriting approved work.

## Minimal Viable Workflow

Default to the smallest workflow that safely satisfies the user. Do not automatically expand a text edit into paper auditing, a figure insertion into full evidence-base construction, or a packaging request into slide content review.

Before task work, choose one mode and mention it briefly:

- `quick_edit`: text, style, or small layout changes that do not require paper evidence.
- `fast_figure_fill`: the user has provided slide-ready assets or the requested figure/table identity is already clear.
- `delivery_package`: the user explicitly asks to package a named version or file for delivery.
- `full_paper_audit`: the user asks for paper download, figure extraction, claim checking, citation audit, broad evidence-grounded revision, or fast mode cannot safely proceed.

Use compact records for `quick_edit`, `fast_figure_fill`, and `delivery_package`. Create full paper manifests, paper summaries, and claim records only in `full_paper_audit`.

## Mode Selection

Always choose one mode before doing task work and mention the choice briefly. Upgrade only when the trigger is present; otherwise keep the workflow narrow.

### Quick Edit Mode

Use this mode for copy edits, small style changes, minor layout adjustments, or fixes that do not depend on paper evidence.

Quick mode does:

- identify the user-named pages or affected local section;
- edit only the requested area;
- export or inspect only the changed pages and necessary adjacent pages;
- write a compact log entry with version, pages, command/output, visual check, and unresolved issues.

Quick mode does not:

- download papers;
- build or update paper manifests;
- generate paper summaries;
- create claim records;
- inspect the whole deck by default;
- generate HTML, PPTX, or full-page screenshot sets unless needed for the requested change.

### Fast Figure Fill Mode

Use this mode by default when the user has already provided the needed figure or table images, screenshots, crops, or other slide-ready assets, and the task is to place them into named pages or placeholders with suitable explanatory text.

Fast mode has two subpaths:

- `provided_asset_insert`: use this when the user-provided asset is the intended figure/table or a user-approved substitute. Do layout, explanation, source note, and local visual checks only.
- `asset_identity_check`: use this when the asset identity is uncertain. Do the minimum evidence lookup needed to confirm or reject the asset before inserting it.

Fast mode does:

- read the named slide pages or explicit placeholders;
- extract the slide's original figure/table requirement, purpose, screenshot suggestion, and surrounding teaching point;
- verify the user-provided asset exists and visually matches the requested paper, figure/table number, or user-approved replacement;
- insert the image/table into the Marp deck without modifying the image pixels unless the user explicitly asks for raster annotation;
- write concise Chinese explanatory text that starts with a traceable reference such as `Author et al. Fig. 1:` or `Author et al. Table 1:`;
- add or preserve a consistent bottom source note;
- export a PDF preview when feasible and inspect only the changed pages plus necessary adjacent pages;
- write a compact version-log entry with changed pages, assets, output files, visual check, and approval status.

Fast mode does not, unless specifically needed:

- download papers;
- extract figures from PDFs;
- build or refresh a full paper manifest;
- generate Chinese paper summaries for every paper;
- fact-check the whole deck page by page;
- run workflow validation samples unrelated to the current edit.

Escalate from fast mode to full mode only when the provided asset is missing or ambiguous, the figure/table identity cannot be verified from the slide requirement and filename/context, the requested explanation requires facts not visible in the image, or the user asks for paper download, figure extraction, fact checking, or full audit work.

### Delivery Package Mode

Use this mode only when the user explicitly asks to package a named Marp version or file for delivery.

Delivery package mode does:

- confirm the exact Marp source and matching PDF requested by the user;
- parse local asset references from Markdown image syntax, HTML `src`/`href`, CSS `url(...)`, and any relevant Marp/YAML local image fields;
- verify that local asset paths are relative and resolve from the Marp file's directory;
- create a zip that preserves the relative directory relationship required by the source deck;
- extract the zip to a temporary validation folder and verify the references again;
- remove staging/validation folders after verification, leaving only the final zip unless the user asks otherwise.

Delivery package mode does not:

- edit Marp content;
- regenerate the PDF unless the user asks;
- run Placeholder Requirements Gate;
- build evidence records;
- inspect slide layout or claims beyond path portability.

### Full Paper Audit Mode

Use this mode when the user asks Codex to download or organize papers, extract figures/tables from PDFs, fact-check slide claims, generate paper summaries, audit citations, revise broad paper-grounded content, validate the whole workflow, or when fast mode cannot safely satisfy the request.

Full mode includes the evidence base, fact-checking records, paper manifest, Chinese paper summaries, figure extraction or cropping, versioned slide edits, PDF preview, visual inspection, and workflow records described below. Build the evidence base incrementally: first list papers and gaps, then download, summarize, and claim-check only within the user-approved scope.

## Core Rules

- Preserve user work. Never overwrite the source deck directly; create a versioned working copy and outputs.
- Edit only pages the user names or pages containing explicit placeholders such as `图表占位`, unless the user approves broader edits.
- Treat each slide's original `用途`, `截图建议`, and named figure/table as binding requirements. Do not substitute a visually convenient figure, full image, generated image, or redraw unless it satisfies those requirements or the user explicitly approves the change.
- Keep privacy out of reusable records. Do not hard-code personal names, local home paths, course folders, credentials, or private URLs in skill outputs.
- Prefer traceable evidence over polished prose. Every factual claim kept in the deck should be supported, corrected, labeled as inference, or marked unresolved when full audit mode is active.
- Treat PDF as the final preview/export artifact. Use inline HTML/CSS/SVG only as a Marp drawing method; keep standalone HTML only when needed for inspection or debugging.
- Keep the user role narrow: request requirements, ask for missing papers or factual approvals, and ask for final visual approval.
- Use UTF-8 for all reusable Markdown records. If existing records are garbled, rewrite the touched reusable document as readable UTF-8 rather than extending the corrupted text.

## Placeholder Requirements Gate

Before filling or replacing any figure placeholder, extract and record the slide's original requirement block:

- slide page number;
- exact `图表占位` text, including paper, figure, or table number;
- exact `用途`;
- exact `截图建议`;
- surrounding slide argument or teaching point;
- selected workflow mode: `fast_figure_fill` or `full_paper_audit`.

Use this block as a blocking checklist. The selected asset must match the requested paper figure/table, the stated purpose, and the screenshot suggestion, unless the version log records the user's approved deviation.

When the user provides the figure/table image, treat that file as the selected asset in fast mode. Do not reverse-engineer the asset from the PDF or download papers just to duplicate the user's file. Preserve the user-provided image as the traceable source asset, and add Chinese labels, callouts, or reading guides in Marp Markdown/HTML/CSS around the image rather than modifying pixels unless raster annotation is explicitly requested.

When full mode is active, preserve the complete requested figure/table as a clean source asset and use the complete figure when the user provides it or asks for it. Create a local crop only when the slide requirement still calls for a crop and the user has not overridden that choice. If no asset can satisfy the requirement block, stop and report the missing asset or ambiguity instead of fabricating a replacement.

## Fast Figure Fill Workflow

1. Scope the edit:
   - Identify the latest approved or user-requested base deck.
   - Create the next versioned working Markdown and matching output names.
   - Limit edits to user-named pages and explicit placeholders.

2. Read placeholder requirements:
   - Capture page number, `图表占位`, `用途`, `截图建议`, and teaching point.
   - Record the user-provided asset path and the figure/table identity it is expected to represent.

3. Insert and explain:
   - Use the provided image/table asset directly.
   - Keep the asset readable and within margins.
   - Write a standalone Chinese explanation beginning with `Author et al. Fig. X:` or `Author et al. Table X:`.
   - Add one consistent source footer:
     `来源：Author et al., Paper Title, Venue, Year, https://...`

4. Compile and inspect:
   - Export PDF when feasible.
   - Inspect changed pages and necessary adjacent pages as PDF or PNG for margins, readability, overlap, font consistency, and source-footer placement.
   - If PDF export fails, first record the failure and determine whether the issue is unrelated to asset paths; use a browser fallback only when the user accepts that path or the project has already validated it.

5. Record and pause:
   - Update a compact version log with changed pages, asset paths, compile command, output PDF, visual check, approval status, and unresolved issues.
   - When the user asks to inspect before continuing, stop after producing the PDF and do not perform extra audit work.

## Full Paper Audit Workflow

1. Create a versioned workspace:
   - Detect the source `.md`/`.marp.md`.
   - Create `workflow_outputs/` with `papers/`, `figures/`, `artifacts/`, and `versions/` or an equivalent project-local structure.
   - Copy the source deck to a timestamped or semver-style working file before editing.
   - Record each formal iteration in `workflow_outputs/version_log.md` or an equivalent project-local version log with deck version, changed pages, reason, commands, outputs, visual checks, and approval status.

2. Build the evidence base:
   - Identify referenced papers from the deck and meeting notes, then list missing PDFs, citation gaps, and claims needing audit before expanding work.
   - Download or use user-provided PDFs. If publisher download fails, use arXiv or another repository only after confirming title, authors, year, DOI, and version match.
   - Create a paper manifest with title, authors, venue, year, DOI/arXiv, source link, local filename, and verification status.
   - Generate a Chinese paper summary for every downloaded or user-provided paper and save it to `workflow_outputs/paper_summaries.md`. Each summary should be 150-300 Chinese characters and cover the research question, method or experiment design, core findings, relevance to the deck, and a human verification entry point.
   - For detailed fields, read `references/fact-checking.md`.

3. Fact-check the deck:
   - Work page by page within the user-approved scope.
   - For each key claim, capture: slide page, slide text, source paper, original excerpt, exact location, conclusion, and action.
   - Classify each claim as supported, needs correction, inference/extension, or unresolved.
   - Provide a human verification path using local PDF filename, page/section/figure/table, and short original excerpt.

4. Revise figures and layout:
   - Apply the Placeholder Requirements Gate before choosing each figure, crop, annotation, redraw, or generated image.
   - Use paper originals for empirical results and named figure placeholders.
   - Use cropped originals or simplified redraws only when the original is too dense, while preserving a source note.
   - When a placeholder asks for labels or annotations, keep the paper image clean and add labels with Marp Markdown/HTML/CSS. Use raster annotation only when explicitly requested or when Marp-rendered labels cannot meet the visual requirement.
   - Write figure explanations with a traceable opening such as `Author et al. Fig. 1:` or `Author et al. Table 1:`. Do not start with generic labels such as `读图：`.
   - Make every figure explanation stand alone: a reader should understand what the figure means from the image plus the explanation, without relying on presenter narration.
   - Use HTML/CSS/SVG inside Marp for concepts, mechanisms, and process diagrams.
   - Use generated bitmap images only for strongly visual or illustrative needs.
   - Put every source note on the slide bottom line in the consistent source format.
   - For layout checks and page rules, read `references/marp-layout.md`.

5. Compile and inspect:
   - Prefer VS Code local Marp preview when available.
   - Always verify Marp CLI export when feasible: compile the working Markdown to PDF with local files enabled if images are embedded.
   - Verify the online editor path only as a fallback workflow when requested or when portability is part of the task.
   - Inspect representative pages visually, including changed pages, pages affected by shared CSS/theme changes, boundary margins, image readability, font consistency, and source footer placement.
   - Do not mark a page complete until the exported PDF/PNG confirms the asset and explanation still satisfy the original `用途` and `截图建议`.

6. Validate automation samples only when validating the workflow itself:
   - Run two or three representative pages through the full loop only when the task is to test or improve the workflow or skill itself.
   - Include one paper-original figure page, one generated/HTML concept page, and one complex layout page when such pages exist.
   - Record exact slide page numbers, changed files, commands, outputs, approval points, and rework count.
   - Do not run this step for ordinary fast figure-fill edits.

7. Deliver:
   - Deliver by mode: quick edits provide the requested Marp/PDF or specified output; fast figure fills provide the updated version, PDF preview, and compact log; delivery packaging provides the zip and path-validation result; full audits additionally provide manifest, summaries, fact-check records, and workflow validation records when produced.
   - Include Marp environment validation conclusion and fallback path only when relevant.

## Version Management

Read `references/versioning-and-safety.md` before substantial edits, multi-round revisions, or any task involving privacy/security constraints. Do not overwrite an approved version; derive the next version number from the latest approved Markdown/PDF pair.

If the user asks to delete or redo a version, preserve the audit trail: mark the old version as `rejected`, `deprecated`, or superseded in the log, then create the replacement as a new version unless the user explicitly asks for local cleanup of unapproved temporary files.

## Useful References

- Read `references/fact-checking.md` when extracting claims, building a paper manifest, preparing human verification materials, or deciding whether fast mode must escalate to full mode.
- Read `references/marp-layout.md` when editing slides, inserting user-provided figures, generating figures, validating PDF output, or comparing VS Code/CLI/online Marp workflows.
- Read `references/versioning-and-safety.md` when setting up output folders, naming versions, recording iterations, replacing/rejecting versions, or sanitizing deliverables.
