---
name: obsidian-note-creating
description: "Create or rewrite a durable Obsidian note with ## Story, naming preamble, and pressure-driven narrative. Use when: create a note, write a note, rewrite this note, make a durable note, story-led note, new knowledge base entry."
---

# Obsidian Note Creating

Create or rewrite a durable Obsidian note. The output is a well-structured note with a naming preamble, a pressure-driven `## Story`, and closing sections for guarantee, boundary, and final mental model.

## What to do

1. Read `references/style-rules.md` for all formatting and structural rules.
2. Read `references/family-routing.md` to choose the right note family (concept, flow, recipe, relationship, index, etc.).
3. Read `references/story-patterns.md` for the pressure-driven story pattern.
4. Search the vault for an existing note on the topic before creating a new one.
5. **For patches to existing notes — snapshot first**: read the file and record the current heading levels, section names, and key content before making any edit. This snapshot is the baseline for step 8.
6. Write or rewrite the note following the rules below.
7. **Wire outgoing links** — scan every concept name in the finished note. For each one that has a vault note, replace plain text or backtick code with `[[note name]]` or `[[note name|display text]]`. Never leave a linkable concept as raw text.
8. **Wire incoming links** — search the vault for existing notes that mention this note's concept by name without a wikilink to it. At the first strong mention in each such note, add `[[this note's name]]`. Add only strong links — skip notes where the mention is passing or incidental.
9. **Verify completion** — before finishing, explicitly confirm all of the following or state why each does not apply:
   - [ ] Outgoing links wired (step 7 done)
   - [ ] Incoming links wired (step 8 done)
   - [ ] Creation logged in `Wiki Ops/logs/YYYY-MM/YYYY-MM-DD.md` (new notes only)
   - [ ] All reported changes verified against the pre-patch snapshot (step 5) — never claim credit for pre-existing content

## Non-negotiable rules

- When a durable note benefits from fast interview review or quick later re-entry, add a concise `## Recap` at the front before the naming preamble. Use a few high-signal bullets for the root rule, the main contrast, and the common trap. Do not add `## Recap` mechanically to every note; use it when it improves quick recall.
- Every durable note starts with a **naming preamble** before `## Story` — say what the name stands for and why it fits the concept.
- `## Story` uses the pressure-driven pattern: pressure → naive idea → breakage → refined rule → why it fits → implementation → guarantee/boundary → final mental model.
- Do NOT create a `### The refined rule` subsection — let the rule emerge as the next paragraph after the breakage.
- Closing sections (`## Common bug`, `## Final mental model`, `## Guarantee and boundary`, `## Limit`, `## Trade off`, `## Human-side control surface`) are top-level `##`, never `###` nested inside `## Story`. Use `## Limit` when the concept has a distinct scope or applicability boundary worth separating from the story. Use `## Trade off` when the tradeoff deserves its own scannable section rather than being buried in the story.
- Never wrap a wikilink in backticks — including C++ attributes like [[likely]], [[unlikely]], [[noreturn]].
- Do not self-link the note. Use **bold** for the note's own name in prose. Example: inside the `SO_REUSEADDR` note, write **SO_REUSEADDR**, not `[[SO_REUSEADDR]]`.
- Log only note **creation** in `Wiki Ops/logs/YYYY-MM/YYYY-MM-DD.md` — patches and rewrites are not logged.
