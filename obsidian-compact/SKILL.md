---
name: obsidian-compact
description: "Compact an already-digested Obsidian note into a cheat-sheet style note. Use when the user asks to compact, trim, condense, or make a note concise after they already understand the deduction process."
---

# Obsidian Compact

## Purpose

Use this skill to rewrite an existing Obsidian note after the learner has already digested it. The goal is not to teach from first principles again; the goal is to preserve fast recall.

## Workflow

1. Read the current note first.
2. Preserve the note's correct conclusions, key code shapes, important wikilinks, figures/images, and dangerous traps.
3. Delete the long deduction path: pressure build-up, repeated examples, step-by-step proof, and explanatory scaffolding.
4. Keep only necessary background: the smallest root fact needed to make the cheat sheet understandable later.
5. Rewrite in the vault's durable-note style unless the target note family has a local exception.
6. Do not log note rewrites; log only new note creation if a new note is explicitly created.
7. Verify by rereading the final note, checking word count, and scanning for broken table/wikilink syntax.

## Output Shape

Prefer this shape for normal concept notes:

1. Concise core ideas list at line 1.
2. One short naming/root sentence.
3. A compact `## Story` or `## Core Rule` section only if it adds recall value.
4. Direct practical sections such as `## When needed`, `## Code shape`, `## Boundary`, or `## Cost`.
5. `## Common Trap` in Q/A form.
6. `## Final mental model`.

Use fewer sections when the note is simple.

## What To Remove

- Long proof chains the learner no longer needs.
- Repeated examples that prove the same point.
- Narrative transitions like "the pressure is..." when they do not add recall value.
- Historical background unless it prevents a common mistake.
- Decorative related links at the bottom.

## What To Keep

- The exact rule.
- The exact failure mode.
- One minimal code example if code is the easiest memory hook.
- Important boundary conditions.
- Low-latency or interview takeaways if already present and useful.
- Existing figures/images unless the user explicitly asks to remove them.

## Markdown Rules

- In tables, do not use unescaped aliased wikilinks like `[[path|display]]`; use `[[path\|display]]` or non-aliased `[[path]]`.
- Prefer visually aligned pipe tables for teaching tables.
- Never wrap wikilinks in inline-code backticks.
