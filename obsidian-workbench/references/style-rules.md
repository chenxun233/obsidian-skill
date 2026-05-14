# Note Style Rules

Apply these after routing chooses the note family.

## Story Presence
- Durable notes should include `## Story`.
- In `## Story`, say what the concept essentially is, not only what it does.
- At the very beginning, say what the thing is generally used for so the reader gets a hands-on bridge early.
- Merge definition into the story by default; do not create a separate `## Definition` section unless the task clearly needs it.
- Use `## Story` for the governing root. Do not force every important subquestion to stay inside it when the note becomes clearer with sibling `##` sections.
- In each note, provide examples when they are needed to make the concept touchable. The reader should be able to see the exact way to apply, use, or implement the idea instead of stopping at abstract story alone.
- When the concept has a programmer-visible, operator-visible, or user-visible interaction surface, include an explicit section that lands on that human side. Say what can be directly controlled, how to do it, give a small example when useful, and if there is no direct control surface, say that plainly and explain what mechanism acts instead.
- Do not use a wikilink to the note itself inside that note. When the note needs to say its own name, use bold text for the local note name instead of a self wikilink.
- When several constraints, causes, options, consequences, or examples are parallel peers, do not compress them into one long sentence. Break them into visible list items so the peer structure is easy to scan. Use bullets for unordered peers and numbered items only when explicit indexing or the local note pattern makes numbering useful.

## Naming preamble
- Before the `## Story` heading, every durable note should include a brief naming line that says what the note's name stands for (expanding abbreviations like `seq_cst` → "sequentially consistent") and why that name fits the concept.
- Place this either as the second sentence of the opening practical-use bridge line, or as a short standalone paragraph between the bridge and `## Story`. Always before `## Story` begins.
- Even when the name is not abbreviated, say where it comes from when the etymology helps anchor the concept — for example, `acquire` and `release` come from lock semantics, `relaxed` comes from "relaxed memory model".
- Goal: the reader should never have to memorize an opaque token. If they grasp the name, they have already started understanding the concept.
- Skip only when the name is fully self-evident (e.g., a plain English noun whose meaning matches the concept exactly with no extra etymology to add).

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
- For durable notes in general, use the pressure-driven story pattern as a natural problem-solving flow, not a rigid checklist: concrete problem frame and practical use -> simplest idea or naive reading -> exact breakage, ambiguity, or failing case -> refined rule or added mechanism -> why that rule fits this environment -> exact implementation or operational landing -> guarantee, non-guarantee, and safety boundary -> final mental model.
- Do NOT create an explicit `### The refined rule` subsection. The refined rule should emerge naturally as the next beat after the breakage. Calling it out as a labeled section makes the structure feel mechanical. Write the insight as the next paragraph; the reader will feel it land.
- The `## Story` section contains only the causal narrative beats (`###` subsections). Structural closing sections — human-side control surface, guarantee and boundary, final mental model — are top-level `##` sections that follow `## Story`, not `###` subsections nested inside it. A note typically ends with `## Human-side control surface`, `## Guarantee and boundary`, and `## Final mental model` at `##` level.
- Treat that pattern as an outline to refer to. The goal is that the reader finishes with a solid grasp of what the thing is, why it exists, what problem it solves, why it reached the current state, and how one stage leads to the next without hidden jumps.
- The background should arrive first and stay brief, but it should not be vague. Show the surrounding system, actor, data path, resource limit, or decision pressure that makes the local reasoning necessary before you start the derivation.
- For design notes, use the designer's version of that same pattern: concrete pressure -> simplest workable idea -> pictured failure or unfairness -> new mechanism -> why that mechanism fits the hardware or workflow -> guarantee and remaining tradeoff/boundary -> final shape.
- In design notes, weave the story as one continuous growth path from beginning to end. Do not present the final module split, final signal partition, or final abstraction first and then explain its parts. Let the final structure appear only after the earlier pressure and fixes make it necessary.
- Use multiple `###` subsections when they make the story beats visible. This is not only for large design notes. Even a short atomic note should use visible `###` beats when that helps the reader feel the causal ladder instead of facing one dense block of logic. Extra detail is good when it is carrying the causal chain forward; do not over-compress a design note until the logic turns into a thin summary.
- When the note has major practical follow-up questions, move them into sibling `##` sections after the story. Good examples are `## Programmer Interaction`, `## Who usually enters ...`, `## What ends ...`, `## Boundary`, or another direct question the reader is likely to ask next.
- For concept or syntax notes, the "new mechanism" step may be a clearer interpretation rather than a hardware block or structural change. The root is still the same: old reading fails, so the note introduces the rule that repairs it.
- Start from the obvious idea or naive mental model when that helps the reader feel the problem.
- Make each next section earned: `pressure -> naive move -> visible breakage -> needed insight -> exact rule -> boundary`.
- Show the internal logic in direct language. The reader should feel why the next paragraph has to exist.
- If the reader would feel a jump between two stages, add the missing bridge instead of compressing it away.
- If you use a compressed phrase for a hidden constraint or boundary, unpack what is actually shared, blocked, or coupled, and why that fact changes the reasoning.
- If that hidden boundary would still be hard to picture, add a small concrete example before moving on.
- Put concrete examples before the abstract rule when possible, especially for the breakage step.
- When the concept has an implementation shape, command shape, API shape, state transition, or code path the reader is likely to use directly, include a concrete example of that shape instead of leaving the note at definition level.
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
- In Flow notes and Recipe notes, make each important step state the missing artifact or state transition explicitly when it matters:
  - prerequisite -> current step -> obtained handle/value/state -> why that output is needed next
- Do not assume the reader will infer what was obtained. If the step exists to produce a group id, fd, mapped address, ownership relation, enabled mode, or similar artifact, name that output directly.
- Keep Flow and Recipe roles separate. Flow notes should explain the ordered why-this-comes-next chain and link outward when one step needs reusable implementation detail. Recipe notes should hold the step-local code order, variable transitions, and directly usable snippets.
- In foldered Recipe notes that act as parent procedures, prefer short `###` step titles such as `### Align`, `### Bind`, or `### Commit` over long sentence-like step labels. Put the explanatory body under the `###` heading instead of forcing the whole step title to carry the explanation.
- When a parent Recipe hands off to child Recipe notes, the parent should use those short `###` sections as the visible chain and then state the local ladder under each section:
  - prerequisite
  - what you obtain
  - why that obtained thing enables the next step
  - the child Recipe link when one exists

## Link Discipline
- Add only strong links.
- Avoid repeated links that do not add a new local job.
- Reuse the nearest strong root link and add another link only when the local paragraph or checkpoint needs a different landing target.
- Do not self-link the current note. Use bold text for the note's own name when the local prose needs that name.
- When naming reusable kernel functions or similar note-worthy APIs in durable notes, use plain Obsidian wikilinks such as [[local_bh_disable()]] instead of source-style backticks, even if the target note does not exist yet.
- Never wrap a wikilink in backticks. Write [[lock_sock()]], not an inline-code version of that same wikilink, because a wikilink is navigation knowledge rather than a code literal.
- This rule applies to ALL note families: Knowledge base, Flow, Deep, Recipes, Collections, Relationship, Indexes, and learning checklists.
- The wrong pattern appears when the writer confuses a wikilink with a code literal. A wikilink is knowledge navigation, not code. Only wrap C identifiers in backticks when they are NOT wikilinks: `snd_una` (a struct field), `sk->sk_lock` (a member access), `tcp_prot` (a global variable). When the identifier IS a wikilink target, drop the backticks.
- The rule also catches tokens whose surface form happens to use `[[ ]]` brackets, including C++ attributes: [[likely]], [[unlikely]], [[noreturn]], [[nodiscard]], [[fallthrough]], [[maybe_unused]], [[deprecated]]. The `[[ ]]` form IS the Obsidian wikilink form, so wrapping any such token in backticks creates the forbidden in-code-wikilink pattern even when the writer intended it as code syntax. Leave them as raw wikilinks; restructure the prose if you need to refer to one as a literal rather than a navigable concept.
- After writing or editing any note, scan for the pattern backtick plus `[[` and remove the surrounding backticks from every wikilink found.
- When a function or API already appears as a wikilink in the note's header relation table (Upper, Sibling, Related, Used in columns), do NOT repeat it as a wikilink in prose. Instead use `**bold**` for that name in the body text. The header table is the one canonical link; a second wikilink in the prose is noise.
- When a function or API does NOT appear in the header relation table, link it as `[[name()]]` on first meaningful use in prose as usual.

## Sequence Diagrams
- When a note or answer contains a time-ordered exchange between two or more named actors — handshake steps, protocol flows, request-response pairs — use a Mermaid `sequenceDiagram` block instead of a prose list or numbered bullets.
- Example trigger: "client sends SYN; server replies SYN-ACK; client sends ACK" → write:
  ````
  ```mermaid
  sequenceDiagram
      Client->>Server: SYN
      Server->>Client: SYN-ACK
      Client->>Server: ACK
  ```
  ````
- Use `->>` for messages that expect a reply (requests), and `-->>` for replies. Add `Note over` or `Note right of` annotations when a state change needs to be visible at that moment.
- Apply this rule in both durable notes and query answers when the exchange has three or more steps or two or more actors.

## Family Shape
- Keep command families in same-name folders.
- Keep class/function/member note families in same-name folders that preserve the code shape.
- Preserve any local bullet or numbering pattern the user establishes inside a note.
