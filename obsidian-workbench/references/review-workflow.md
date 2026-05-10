# Note Review Workflow

Use this workflow for any Obsidian note creation or note modification.

## Teacher And Student
- The writer is the teacher.
- The teacher creates or patches the note so it teaches from common root to direct use.
- Then run one combined student reviewer when subagents are available.
- If subagent creation fails because the session hit an agent-thread limit, close stale or finished agents and retry once before treating subagents as unavailable.

## Combined Reviewer Lenses
The combined student reviewer must check all three lenses in one pass:
- Truth lens: current, technically accurate, not misleading, not duplicated
- Use lens: operational usefulness, examples, commands, proof standards, link quality
- Learning lens: clear basic idea, explicit logic, low ambiguity, solid mental placement

## Ambiguity Reporting
- If wording is ambiguous, the reviewer must report it explicitly as a finding instead of only describing the note as "unclear" in summary.
- Treat ambiguity as any wording that could imply the wrong actor, action, direction, read/write effect, causal relationship, proof boundary, or next step.
- When possible, name the exact ambiguous phrase and say what wrong reading it permits.

## Required Pattern Checks
- Inspect whether reusable kernel functions or similar note-worthy APIs are written as Obsidian wikilinks, not wrapped in source-style backticks.
- Treat `[[local_bh_disable()]]` and `[[local_bh_enable()]]` as the desired pattern, not `` `local_bh_disable()` `` and `` `local_bh_enable()` ``.
- Treat any backtick-wrapped wikilink, such as `` `[[lock_sock()]]` ``, as a finding. Kernel-function knowledge links must render as links, not inline code.
- Apply this check even when the target note does not exist yet; missing-note placeholders are preferred over plain code formatting when the note should be linkable knowledge.

## Integration
- Feed the combined review back into the teacher.
- Patch the note when the reviewer finds ambiguity, duplication, weak links, weak actionability, missing boundaries, or broken story order.

## Fallback
- Simple append-only daily-log edits do not need this workflow.
- If subagents are still unavailable after agent cleanup and one retry, or are blocked by a higher-priority runtime rule, state that exact blocker and do the local review yourself with the same three lenses.
