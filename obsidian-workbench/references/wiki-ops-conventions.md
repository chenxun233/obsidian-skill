# Wiki Ops Conventions

The operational layer keeps the persistent wiki maintainable. There is no central Wiki Ops index; route by searching compiled note families, following strong links, and reading recent logs only when recent context matters.

- `Wiki Ops/lint.md`
 Current maintenance surface: contradictions, stale claims, orphan pages, missing cross-links, and open questions.

- `Wiki Ops/logs/YYYY-MM/YYYY-MM-DD.md`
 Append-only daily files for new note creation activity, grouped by month folder.

Log entry rules:

- Append to the current daily file only when a new note is created.
- Use the file path itself as the date boundary: keep the date in the filename `YYYY-MM-DD.md` and do not repeat a `# YYYY-MM-DD` heading inside the file.
- Do not log edits to existing note content, memory updates such as `AGENTS.md`, or skill modifications.
- If a turn both creates a new note and modifies existing notes, log only the new note creation and mention supporting edits only when needed to understand the new note.
- In that daily file, start each new-note entry with its own level-2 heading that also carries the operation content, for example `## Note: <the note operation content>` or `## Ingest: <normalized new note summary>`, so rendered logs show clear operation boundaries without repeating the content again as a separate subheading line.
- Normalize the operation-content part into one concise summary. Do not copy raw user wording or source wording blindly when it is verbose, slightly mistaken, or not the cleanest stable label for the operation.
- Put operation-specific fields under level-3 headings such as `### Answer`,`### Helpful Links`,`### Persistence Decision`,`### Touched Pages`, or `### Result`.
- Include operation type, created pages, and the main result.
- Read only the relevant recent daily files unless the task explicitly needs older operational history.
