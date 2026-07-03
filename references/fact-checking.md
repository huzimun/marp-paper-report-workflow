# Fact Checking Reference

## Paper Manifest

Create one row per paper with:

- `paper_id`: short stable key, e.g. first author plus year.
- `title`
- `authors`
- `venue`
- `year`
- `doi_or_arxiv`
- `source_url`
- `local_pdf`
- `download_or_user_provided`
- `identity_check`: title/authors/year/DOI or arXiv match status.
- `notes`: publisher access issue, preprint/final mismatch, missing pages, or supplement files.

If using a non-publisher source, confirm it is the same paper by matching title, author list, year, and DOI/arXiv. Record any version mismatch.

## Claim Record

Create one row per slide claim or figure use:

- `slide_page`
- `slide_claim`
- `paper_id`
- `paper_excerpt`: short quote only; avoid copying long passages.
- `location`: PDF page plus section, figure/table number, caption, or nearby heading.
- `classification`: `supported`, `needs_correction`, `inference_or_extension`, or `unresolved`.
- `action`: `keep`, `revise`, `delete`, or `discuss`.
- `human_check`: exactly what a reviewer should open and compare.

For figure use, include original figure/table number, PDF page, caption summary, and whether the slide uses the original, a crop, or a simplified redraw.

## Human Verification Standard

Make the evidence easy for a person to audit without trusting Codex:

1. Provide the local PDF filename.
2. Give a concrete position: PDF page and section/figure/table/caption.
3. Include a short original excerpt or caption fragment.
4. State the slide page and the exact slide wording being checked.
5. State whether the slide wording is directly supported or requires revision.

Do not label unsupported synthesis as fact. Mark derived interpretation as `inference_or_extension` and explain what the source does and does not say.
