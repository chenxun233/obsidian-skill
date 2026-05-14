# Query Routing

Use the wiki in this order.

1. Search compiled note families directly using the user's terms, likely aliases, and root concepts.
2. Read the relevant concept, source-tied, flow, deep, recipe, issue-record, and relationship pages.
3. Follow strong wikilinks from the best-matching pages to complete the local graph.
4. Check `Wiki Ops/lint.md` if the question may hit stale or disputed material.
5. Read the current daily log under `Wiki Ops/logs/YYYY-MM/YYYY-MM-DD.md` when recent wording or context matters. This file is also the default log target for the new query, and for any note creation or modification made while answering it.
6. Read at most a few recent older daily logs under `Wiki Ops/logs/YYYY-MM/` when the answer may have been asked recently but not today.
7. If a prior query entry already answers the same question well enough, log the repeated query but keep the answer body short — just a link to the prior entry. Example: `See [[Wiki Ops/logs/2026-05/2026-05-13#Query: what flag is used when a TCP packet is sent|prior entry from 2026-05-13]]`. Do not write a full re-answer.

## Logging shape

All logs — query entries, note creation, and note modification — live in one path: `Wiki Ops/logs/YYYY-MM/YYYY-MM-DD.md`. There is no separate `Query/` folder.

- Note creation and modification entries use the one-line form: `**Category:** Verb [[note]] — short reason.` Verbs include Created, Patched, Rewrote, Renamed. Keep entries short — one line per note, no paragraph-length descriptions.
- Query entries use the `## Query: <normalized summary>` heading with `### Answer`, `### Helpful Links`, and `### Persistence Decision` subsections. They sit below the day's note-creation/modification lines.
- Memory updates (`AGENTS.md`) and skill modifications are NOT logged.

Do not treat the daily logs as the primary knowledge source. The compiled pages are primary. There is no default learning-checklist layer for queries; reusable query results should become durable compiled notes directly.
