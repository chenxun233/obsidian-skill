---
name: obsidian-query
description: "Answer a question from the compiled Obsidian wiki. Use when: what is X, how does Y work, explain Z, look up this concept, search my notes, find the note about, wiki question."
---

# Query

Answer a question by searching the maintained Obsidian wiki. Search compiled notes first, then query history only when recent wording matters. Persist reusable answers back into durable notes when the answer uncovers a gap.

## What to do

1. Read `references/query-routing.md` for the search order and logging shape.
2. Search compiled note families directly using the user's terms, likely aliases, and root concepts.
3. Read the relevant concept, flow, deep, recipe, and relationship pages.
4. Follow strong wikilinks from the best-matching pages to complete the local graph.
5. Check `Wiki Ops/lint.md` if the question may hit stale or disputed material.
6. Read the current daily log `Wiki Ops/logs/YYYY-MM/YYYY-MM-DD.md` when recent context matters — this is also the log target for this query.
7. If a prior query entry answers the same question well enough, link to it and keep the new answer short.

## Logging shape

Log the query as `## Query: <normalized summary>` with `### Answer`, `### Helpful Links`, and `### Persistence Decision` in the current daily log. Use the one-line creation form for any note created while answering. Do not log patches or rewrites.
