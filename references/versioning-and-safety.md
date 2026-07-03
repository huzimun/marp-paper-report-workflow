# Versioning and Safety Reference

## Versioned Outputs

Never edit the source deck as the only copy. For formal deck revisions, prefer incremental versions:

- Iteration: `deck.workflow-v01.marp.md`, `deck.workflow-v02.marp.md`
- Current candidate: `artifacts/deck.current.marp.md`
- Formal history: `versions/deck.workflow-vNN.marp.md`

Keep generated PDFs tied to the Markdown version by matching names.
Do not overwrite an approved version. Start each new round by copying the latest approved Markdown/PDF pair to the next version number, then edit only the new version.
Keep `artifacts/` for current candidates, temporary exports, and inspection files; keep `versions/` for formal history.

## Iteration Log

Maintain `workflow_outputs/version_log.md` or an equivalent project-local log. Record each formal revision with:

- version id
- date/time
- source deck
- working deck
- changed slide pages
- user request or approval point
- files changed
- figure assets created or updated
- compile command
- output PDF
- visual check result
- approval status: `pending`, `approved`, or `rejected`
- unresolved issues

If a user reports a problem, add the report and the fix attempt to the log rather than silently replacing history.

## Privacy and Security

- Do not include personal home paths, usernames, private course folder names, access tokens, cookies, or internal URLs in reusable skill files or final public summaries.
- In project-local records, prefer relative paths such as `workflow_outputs/papers/...`.
- Redact private paths from examples before turning them into reusable templates.
- Do not upload private PDFs or decks to online editors unless the user explicitly approves and the privacy risk is stated.
- If network download fails, ask for user-provided PDFs or use public repositories only when identity can be verified.

## Change Scope

- Preserve unrelated user edits.
- Do not modify pages without placeholders unless the user names them.
- Do not regenerate artifacts from stale scripts if manual edits have superseded script output; update the script first or compile the current Markdown directly.
- Keep rollback possible by retaining the previous working version before substantial edits.
- Treat `versions/deck.workflow-vNN.*` as immutable after approval. If an approved version needs correction, create `vNN+1` and document the correction.
