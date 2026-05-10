# Note Review Workflow

Use this workflow for any Obsidian note creation or note modification.

## Teacher Workflow
- The writer is the teacher.
- The teacher creates or patches the note so it teaches from common root to direct use.
- The teacher must also perform one explicit self-review pass before the work is treated as complete.

## Required Self-Review Lenses
The teacher self-review must check all three lenses in one pass:
- Truth lens: current, technically accurate, not misleading, not duplicated
- Use lens: operational usefulness, examples, commands, proof standards, link quality
- Learning lens: clear basic idea, explicit logic, low ambiguity, solid mental placement

## Ambiguity Reporting
- If wording is ambiguous, the teacher must treat it as a concrete fix target instead of only calling the note "unclear" in summary.
- Treat ambiguity as any wording that could imply the wrong actor, action, direction, read/write effect, causal relationship, proof boundary, or next step.
- When possible, name the exact ambiguous phrase and say what wrong reading it permits.

## Required Pattern Checks
- Inspect whether reusable kernel functions or similar note-worthy APIs are written as Obsidian wikilinks, not wrapped in source-style backticks.
- Treat `[[local_bh_disable()]]` and `[[local_bh_enable()]]` as the desired pattern, not `` `local_bh_disable()` `` and `` `local_bh_enable()` ``.
- Treat any backtick-wrapped wikilink, such as `` `[[lock_sock()]]` ``, as a finding. Kernel-function knowledge links must render as links, not inline code.
- Apply this check even when the target note does not exist yet; missing-note placeholders are preferred over plain code formatting when the note should be linkable knowledge.

## Integration
- Patch the note when the teacher self-review finds ambiguity, duplication, weak links, weak actionability, missing boundaries, or broken story order.

## Fallback
- Simple append-only daily-log edits do not need this workflow.
- If subagents are still unavailable after agent cleanup and one retry, or are blocked by a higher-priority runtime rule, state that exact blocker and do the same teacher self-review locally.
