# Family Routing

Choose the note family from the main root the reader needs.

- One reusable concept with one governing idea:`Atomic note`
- One standard repeatable procedure:`Flow note`
- One topic that needs longer explanation or wider context:`Deep note`
- One sibling set under one shared root:`Collection note`; save it with a `Collection--` filename prefix.
- One hierarchy or navigation map for a field:`Index note`
- One concrete issue, debugging case, or investigation record:`Ingest Resource Raw/Issues/` record
- One reusable step-by-step procedure extracted from a solved issue, useful command, or engineering practice:`Recipe note` — saved under `Recipes/`, owned by the procedure itself so one Recipe can serve many issue records
- One reusable function or function-shaped building block:`Useful function note`

## Recipe Note Routing

When an issue record contains a concrete solution with strong reusable steps, extract those steps into a standalone `Recipe note` under `Recipes/`. The issue record should then link to the Recipe instead of repeating the reusable procedure inline.

When solving a new issue:
- Search`Recipes/` first for existing Recipes whose symptom pattern or purpose matches.
- If one fits, link to it from the issue record and add only the case-specific context (parameters, values, why it applied).
- If none fits, create a new Recipe only when the procedure is stable enough for next-time reuse.
- If the branch is mainly a caution, weakening result, proof boundary, partial contributor, or case-shaped observation, do not force it into `Recipes/`; keep it in the story, checklist, Deep note, or issue record.

A Recipe note is not owned by any single issue record. It is owned by the procedure. The same Recipe can be linked from many issue records, Knowledge base notes, and Flow notes.

Do not use this skill for these cases:

- Source-derived notes, chapter notes, article ingestion, or former learning-note work: switch to learning checklist ingest mode.
- Compiled-wiki questions, answer-from-wiki tasks, or wiki maintenance passes: switch to compiled wiki query mode.
