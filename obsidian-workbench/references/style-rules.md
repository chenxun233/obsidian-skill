# Note Style Rules

Apply these after routing chooses the note family.

## Story Presence
- Durable notes should include `## Story`.
- In `## Story`, say what the concept essentially is, not only what it does.
- At the very beginning, say what the thing is generally used for so the reader gets a hands-on bridge early.
- Merge definition into the story by default; do not create a separate `## Definition` section unless the task clearly needs it.

## Story Order
- Every story must follow a visible ordering rule.
- Default to one of:
  - logic sequence
  - time sequence
  - easy-to-hard teaching sequence
- The reader should be able to feel why this part comes before the next one.

## Story Construction
- Start from the common root and let each later move grow from the problem created by the earlier move.
- When the user wants a stronger story, narrative, first-principles explanation, or a more natural `## Story`, write it like progressive discovery rather than like a textbook summary.
- For durable notes in general, use the tighter pressure-driven story pattern: concrete problem frame and practical use -> simplest idea or naive reading -> exact breakage, ambiguity, or failing case -> refined rule or added mechanism -> why that rule fits this environment -> exact implementation or operational landing -> guarantee, non-guarantee, and safety boundary -> final mental model.
- The background should arrive first and stay brief, but it should not be vague. Show the surrounding system, actor, data path, resource limit, or decision pressure that makes the local reasoning necessary before you start the derivation.
- For design notes, use the designer's version of that same pattern: concrete pressure -> simplest workable idea -> pictured failure or unfairness -> new mechanism -> why that mechanism fits the hardware or workflow -> guarantee and remaining tradeoff/boundary -> final shape.
- In design notes, weave the story as one continuous growth path from beginning to end. Do not present the final module split, final signal partition, or final abstraction first and then explain its parts. Let the final structure appear only after the earlier pressure and fixes make it necessary.
- Use multiple `###` subsections when they make the story beats visible. Extra detail is good when it is carrying the causal chain forward; do not over-compress a design note until the logic turns into a thin summary.
- For concept or syntax notes, the "new mechanism" step may be a clearer interpretation rather than a hardware block or structural change. The root is still the same: old reading fails, so the note introduces the rule that repairs it.
- Start from the obvious idea or naive mental model when that helps the reader feel the problem.
- Make each next section earned: `pressure -> naive move -> visible breakage -> needed insight -> exact rule -> boundary`.
- Show the internal logic in direct language. The reader should feel why the next paragraph has to exist.
- Put concrete examples before the abstract rule when possible, especially for the breakage step.
- After introducing the fix, say why this fix is cheap, direct, safe, or natural in this environment instead of leaving it as an unexplained choice.
- Land the story back on the actual signals, helper function, syntax form, API surface, command position, or state transition where the rule appears.
- State clearly what the note's mechanism guarantees and what it does not guarantee. If safety depends on an outside assumption, sizing choice, or later stage, say that explicitly.
- Use small critical code or command fragments only at the moment they prove the idea. Do not dump large listings when the local logic only needs a few lines.
- End by reassembling the full picture so the reader can see how the pieces fit.
- Use `###` subsection titles inside stories whenever they help mark the narrative beats. The titles should expose the arc, not just label topics mechanically.
- If one story becomes too large for one note, use a big-story plus focused-side-story pattern: keep the parent note for the governing arc and move durable sub-stories into child notes.

## Teaching Shape
- Start from the common root.
- In diagnostic or procedural notes, use the workflow ladder:
  - previous proof -> current stage -> evidence shape -> permitted conclusion -> forbidden conclusion -> next valid step

## Link Discipline
- Add only strong links.
- Avoid repeated links that do not add a new local job.
- Reuse the nearest strong root link and add another link only when the local paragraph or checkpoint needs a different landing target.
- When naming reusable kernel functions or similar note-worthy APIs in durable notes, use plain Obsidian wikilinks such as [[local_bh_disable()]] instead of source-style backticks, even if the target note does not exist yet.
- Never wrap a wikilink in backticks. The form `` `[[lock_sock()]]` `` is forbidden because it renders as code instead of a link; write [[lock_sock()]].
- This rule applies to ALL note families: Knowledge base, Flow, Deep, Recipes, Collections, Relationship, Indexes, and learning checklists.
- The wrong pattern `` `[[tcp_sk()]]` `` appears when the writer confuses a wikilink with a code literal. A wikilink is knowledge navigation, not code. Only wrap C identifiers in backticks when they are NOT wikilinks: `snd_una` (a struct field), `sk->sk_lock` (a member access), `tcp_prot` (a global variable). When the identifier IS a wikilink target, drop the backticks.
- After writing or editing any note, scan for `` `[[ `` and remove the surrounding backticks from every wikilink found.

## Family Shape
- Keep command families in same-name folders.
- Keep class/function/member note families in same-name folders that preserve the code shape.
- Preserve any local bullet or numbering pattern the user establishes inside a note.
