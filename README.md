# Marp Paper Report Workflow

A Codex skill for versioned, paper-grounded Marp/Markdown academic presentation workflows.

This skill helps Codex turn a paper-based Marp deck into a verifiable and mostly automated workflow: fact-check claims against source papers, organize PDFs, extract or redraw figures, revise slide layout, compile PDF previews, validate Marp environments, and record human-auditable evidence.

## What It Supports

- Paper-grounded fact checking for academic slide decks
- Human-verifiable evidence records with PDF locations and source excerpts
- Figure/table extraction, cropping, simplified redraws, and Marp HTML/CSS/SVG diagrams
- Versioned Marp Markdown and PDF output workflows
- VS Code, Marp CLI, and online editor validation paths
- Privacy-aware workflow records that avoid exposing local paths, credentials, or private materials

## Repository Contents

- `SKILL.md` - primary Codex skill instructions
- `SKILL_zh-CN.md` - Chinese review copy for human inspection
- `references/fact-checking.md` - paper manifest and claim verification schema
- `references/marp-layout.md` - slide layout, figure strategy, and Marp export rules
- `references/versioning-and-safety.md` - iteration, privacy, and safety rules
- `agents/openai.yaml` - Codex UI metadata

## Usage

Install or copy this folder into your Codex skills directory, then invoke:

```text
Use $marp-paper-report-workflow to fact-check and revise this paper-based Marp presentation with versioned outputs.
```

The skill is designed for workflows where the user provides requirements and approvals while Codex performs the evidence tracing, slide edits, figure generation or extraction, PDF compilation, and validation records.

## Safety Notes

Do not upload private PDFs or decks to online editors unless explicitly approved. Keep project records local by default and avoid committing private paths, credentials, or unpublished materials.

## License

MIT License. See `LICENSE`.
