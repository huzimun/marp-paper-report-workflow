# Fact Checking Reference

Use this reference only when the selected mode needs evidence work. Fast Figure Fill Mode uses the lightweight checks below; Full Paper Audit Mode uses the full manifest, summaries, and claim records.

## Fast Mode Evidence Boundary

When the user provides slide-ready figure or table assets, do not download papers or rebuild the evidence base by default. Record only:

- slide page number;
- requested paper and figure/table number from the placeholder or user request;
- provided asset path;
- whether the asset visibly matches the requested figure/table or is a user-approved substitute;
- explanation text added to the slide;
- source footer used on the slide;
- any uncertainty that would require paper lookup.

Escalate to Full Paper Audit Mode when:

- the provided image does not clearly match the requested figure/table;
- the filename, slide placeholder, or screenshot suggestion conflicts;
- the explanation requires a factual claim not visible in the provided asset;
- citation metadata is missing and cannot be inferred from existing deck records;
- the user asks for paper download, figure extraction, claim checking, or full audit.

Fast mode may use already-existing project records such as `paper_manifest.md` or prior slide footers to fill source metadata, but it should not stop the layout task to create missing full audit files unless needed for correctness.

## Paper Manifest

Create or update the manifest in Full Paper Audit Mode. Create one row per paper with:

- `paper_id`: short stable key, e.g. first author plus year;
- `title`;
- `authors`;
- `venue`;
- `year`;
- `doi_or_arxiv`;
- `source_url`;
- `local_pdf`;
- `download_or_user_provided`;
- `identity_check`: title/authors/year/DOI or arXiv match status;
- `chinese_summary`: path or anchor for the paper's Chinese summary in `workflow_outputs/paper_summaries.md`;
- `notes`: publisher access issue, preprint/final mismatch, missing pages, or supplement files.

If using a non-publisher source, confirm it is the same paper by matching title, author list, year, and DOI/arXiv. Record any version mismatch.

## Chinese Paper Summaries

Create `workflow_outputs/paper_summaries.md` after downloading or receiving PDFs in Full Paper Audit Mode. Add one 150-300 Chinese character summary per paper with:

- `paper_id`;
- title, authors, venue, year;
- research question;
- method, task, dataset, or experimental design;
- core findings;
- how the paper supports or frames the deck;
- human verification entry point: local PDF filename plus section, page, figure, or table to inspect first.

Keep summaries concise and audit-friendly. Do not translate the whole abstract. Do not present Codex inference as a paper conclusion; mark uncertain interpretation as `需要复核`.

Do not generate summaries during Fast Figure Fill Mode unless the user explicitly asks for them or the slide explanation cannot be written responsibly without reading the paper.

## Claim Record

Create claim records in Full Paper Audit Mode, or for a fast-mode page only when the inserted explanation makes a non-obvious factual claim.

Create one row per slide claim or figure use:

- `slide_page`;
- `slide_claim`;
- `paper_id`;
- `paper_excerpt`: short quote only; avoid copying long passages;
- `location`: PDF page plus section, figure/table number, caption, or nearby heading;
- `classification`: `supported`, `needs_correction`, `inference_or_extension`, or `unresolved`;
- `action`: `keep`, `revise`, `delete`, or `discuss`;
- `human_check`: exactly what a reviewer should open and compare.

For figure use in full mode, include original figure/table number, PDF page, caption summary, and whether the slide uses the original, a crop, a user-provided asset, or a simplified redraw.

## Human Verification Standard

Make the evidence easy for a person to audit without trusting Codex:

1. Provide the local PDF filename or user-provided asset path.
2. Give a concrete position: PDF page and section/figure/table/caption when a PDF was used; slide page and image filename when a user-provided asset was used.
3. Include a short original excerpt or caption fragment only when the paper was consulted.
4. State the slide page and the exact slide wording being checked.
5. State whether the slide wording is directly supported, visually supported by the asset, requires revision, or is an inference.

Do not label unsupported synthesis as fact. Mark derived interpretation as `inference_or_extension` and explain what the source does and does not say.
