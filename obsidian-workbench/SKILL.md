---
name: obsidian-workbench
description: "Unified Obsidian vault work in one installable skill: read or search vault content, create or revise durable notes with `## Story`, build learning checklists from raw sources including PDF sources, answer from a maintained Obsidian wiki, fix Obsidian Markdown syntax, edit Bases `.base` files, use the Obsidian CLI, or debug Obsidian code-block CSS issues. Use when you want one portable Obsidian skill pack instead of many separate folders."
---

# Obsidian Workbench

Use this as the single entry skill for Obsidian-related work.

It bundles the old vault read/search, note-writer, wiki-ingest, wiki-query, markdown, bases, CLI, and Code Styler workflows into one portable folder.

## Core Rule

- Pick the mode from the main output, not from the file extension alone.
- Search existing vault content before creating a new note or checklist.
- Load only the references needed for the chosen mode.
- Keep paths portable: use files bundled in this skill, not machine-specific absolute paths.
- If the target vault has local rules in `AGENTS.md` or similar project memory, let those override the generic defaults here.

If the task boundary is unclear, read `references/mode-routing.md` first.

## Modes

### 1. Vault read/search mode

Use for simple read, list, grep, or one-off note lookup work.

- Prefer this mode when no durable note-writing workflow is needed.
- If the request turns into maintained note creation or revision, switch to durable note mode.

### 2. Durable note mode

Use when the main output is a durable Obsidian note revision or creation.

- Read `references/family-routing.md`, `references/style-rules.md`, `references/story-patterns.md`, `references/recipe-policy.md`, and `references/review-workflow.md`.
- Route by governing root: note family first, then note structure.
- In each note, not only the story but also the concrete implementation path matters. Provide examples when they are needed so the reader can see the exact way to apply or implement the concept, not only the abstract explanation.
- When the concept has a programmer-visible or operator-visible interaction surface, include an explicit human-side control/interaction section. State what can be directly controlled, exactly how, and if nothing direct is exposed, say that and explain what mechanism acts instead.
- Do not self-link the note name inside the note. When the note needs to refer to itself, use bold text for its own name instead of a wikilink to itself.
- When several constraints, causes, options, or consequences are parallel peers, do not bury them in one long sentence. Break them into visible list items. Use bullets for unordered peers and numbered items only when explicit indexing or the local note pattern makes numbering useful.
- Use `## Story` for the governing root. If the note also needs direct landings such as who enters a state, what ends it, what a programmer can control, or another practical boundary, promote those into sibling `##` sections instead of forcing everything into `## Story`.
- For `## Story`, use the pressure-driven story pattern as a natural problem-solving flow, not a rigid checklist:
  concrete problem frame and practical use -> simplest idea or naive reading -> exact breakage or failing case -> refined rule or added mechanism -> why that rule fits this environment -> exact implementation or operational landing -> guarantee, non-guarantee, and safety boundary -> final mental model.
- Treat that pattern as an outline to refer to. The reader should finish with a solid grasp of what the thing is, why it exists, what problem it solves, why it became the current state, and how each stage leads to the next without hidden gaps.
- When a story introduces a concrete object, file, sysfs node, API, struct, or command as the answer, first explain what new question or pressure made the reader need that object at all. Do not jump straight from failure case to object anatomy without showing why the story had to go looking for that object.
- For system or design topics, use the designer-thought form of the same pattern:
  concrete pressure -> simplest workable idea -> pictured failure or unfairness -> mechanism that fixes that specific problem -> why this fix fits the hardware/workflow -> guarantee and remaining boundary -> final shape.
- Only log new note creation when the target vault's workflow requires it. Do not log ordinary edits unless the vault rule explicitly says to.

### 3. Learning checklist ingest mode

Use when raw material should become a reusable learning checklist rather than a compact durable note.

- Read `references/source-modes.md`, `references/story-led-checklists.md`, `references/wiki-ops-conventions.md`, and `references/review-rubric.md`.
- If the source is a PDF, also read `references/pdf-ingest-workflow.md` before extracting or summarizing.
- Treat the source as immutable.
- Prefer revising the matching checklist over creating a duplicate.
- Keep the checklist incremental and story-led, with checkpoints attached where the learner now needs them.

### 4. Compiled wiki query mode

Use when the maintained wiki should answer a question or when the wiki needs maintenance.

- Read `references/query-routing.md` and `references/persistence-heuristics.md`.
- Search durable notes first, then any query history only when wording or prior answers matter.
- Persist reusable knowledge back into durable notes when the answer uncovers a durable gap.

### 5. Markdown syntax mode

Use when the task is mainly about Obsidian Markdown syntax rather than note-family choice.

- Limit this mode to frontmatter, wikilinks, embeds, callouts, block references, Mermaid, comments, footnotes, or rendering caused by syntax.
- If the task is actually about note structure or story clarity, switch to durable note mode.

### 6. Bases mode

Use for Obsidian Bases `.base` files.

- Read `references/FUNCTIONS_REFERENCE.md` when formulas or functions are involved.
- Define filters first, then views, then formulas and summaries only where they are displayed or reused.
- Validate YAML and formula references after edits.

### 7. CLI and plugin-debug mode

Use when the task needs a running Obsidian instance, plugin reload, DOM inspection, screenshots, console errors, or theme/plugin debugging.

- Use the Obsidian CLI and dev commands.
- Treat app-side inspection as the source of truth for rendering or plugin-state bugs.

### 8. Code Styler CSS-fix mode

Use for fenced code-block styling problems involving themes, CSS snippets, or the Code Styler plugin.

- Patch narrowly.
- Check enabled snippets first.
- Prefer live DOM or rendered evidence before broad CSS changes.

### 9. Figure prompt mode

Use when the user wants an image prompt to visualize a concept, relationship, or process for an external image-generation tool (ChatGPT, DALL-E, Midjourney, etc.).

- Read `references/figure-prompt.md`.
- Identify the main concept and any supporting concepts that help understanding, even if the user did not ask for them.
- Produce a self-contained prompt the user can paste directly into an image tool — no explanation needed, just the prompt.
- Keep the figure simple: one core relationship, minimal text, labeled boxes and arrows, clean style line at the end.

## Mode Escalation

- Simple vault lookup -> vault read/search mode
- Durable note or `## Story` rewrite -> durable note mode
- Source to learning checklist -> learning checklist ingest mode
- Maintained wiki answer or maintenance -> compiled wiki query mode
- Syntax-only Markdown fix -> markdown syntax mode
- `.base` work -> bases mode
- Running app commands or plugin/theme debugging -> CLI and plugin-debug mode
- Fenced-code CSS issue -> Code Styler CSS-fix mode
