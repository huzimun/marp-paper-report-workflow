# Versioning and Safety Reference

## Versioned Outputs

Never edit the source deck as the only copy. For formal deck revisions, prefer incremental versions:

- Iteration: `deck.workflow-v01.marp.md`, `deck.workflow-v02.marp.md`
- Current candidate: `artifacts/deck.current.marp.md`
- Formal history: `versions/deck.workflow-vNN.marp.md`

Keep generated PDFs tied to the Markdown version by matching names.
Do not overwrite an approved version. Start each new round by copying the latest approved Markdown/PDF pair to the next version number, then edit only the new version.
Keep `artifacts/` for current candidates, temporary exports, and inspection files; keep `versions/` for formal history.

## Redoing or Deleting Versions

If the user says to delete, replace, or redo an existing version, preserve the audit trail unless they explicitly request cleanup of temporary files.

- For an approved version, never delete or overwrite it. Create the next version and record that it supersedes the earlier one.
- For an unapproved formal version, prefer marking it `rejected`, `deprecated`, or `superseded` in `version_log.md`, then create the replacement version.
- For temporary artifacts under `artifacts/`, cleanup is allowed when the user asks for cleanup and the files are not the only record of an approved output.
- If a version was mistakenly created from the wrong base, record the mistake and the corrected base in the next log entry.

## Iteration Log

Maintain `workflow_outputs/version_log.md` or an equivalent project-local log. Use UTF-8. If a log is already garbled, rewrite touched entries as readable UTF-8 rather than appending more corrupted text.

For every formal revision, record:

- version id;
- date/time;
- workflow mode: `fast_figure_fill` or `full_paper_audit`;
- source deck;
- working deck;
- changed slide pages;
- user request or approval point;
- files changed;
- figure assets created, extracted, or user-provided;
- compile command;
- output PDF;
- visual check result;
- placeholder compliance: original `图表占位`, `用途`, `截图建议`, chosen asset, and whether the exported result matches them;
- approval status: `pending`, `approved`, `rejected`, `deprecated`, or `superseded`;
- unresolved issues.

Fast Figure Fill Mode may use a compact log entry, but it must still include changed pages, selected assets, output PDF, visual check, and approval status.

If a user reports a problem, add the report and the fix attempt to the log rather than silently replacing history.

## Privacy and Security

- Do not include personal home paths, usernames, private course folder names, access tokens, cookies, or internal URLs in reusable skill files or final public summaries.
- In project-local records, prefer relative paths such as `workflow_outputs/papers/...`.
- Redact private paths from examples before turning them into reusable templates.
- Do not upload private PDFs or decks to online tools without explicit approval.
- If network download fails, ask for user-provided PDFs or use public repositories only when identity can be verified.
- Public README files and reusable templates should use generic paths such as `project-folder/` instead of a user's local course directory.

## Change Scope

- Preserve unrelated user edits.
- Do not modify pages without placeholders unless the user names them.
- Do not regenerate artifacts from stale scripts if manual edits have superseded script output; update the script first or compile the current Markdown directly.
- Keep rollback possible by retaining the previous working version before substantial edits.
- Treat `versions/deck.workflow-vNN.*` as immutable after approval. If an approved version needs correction, create `vNN+1` and document the correction.
- In Fast Figure Fill Mode, do not let evidence-building tasks expand the scope unless they are required to safely complete the named slide edits.
