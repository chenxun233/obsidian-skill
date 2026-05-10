# Story Patterns

Use these patterns when a note should teach through a strong `## Story` instead of only summarizing facts.

## General Durable-Note Pattern

Use this as the default pattern for atomic durable notes of any kind: concepts, syntax, commands, APIs, mechanisms, or designs.

1. Start from the concrete problem frame and practical use.
   First bring in the background, but do it concretely: what surrounding system, actor set, workflow, resource, or decision pressure makes this note exist. Then say what the thing is generally used for, so the reader gets a hands-on bridge immediately.

2. Start from the simplest idea or naive reading.
   Use the version a smart learner or designer would naturally believe first.

3. Show the exact pressure that breaks that first reading.
   Use a pictured failing case, ambiguity, exception, hidden actor, or missing boundary. The reader should be able to point at what goes wrong, not just hear that something is "insufficient."

4. Introduce the refined rule.
   For design notes, this may be a new mechanism. For concept or syntax notes, this may be the interpretation that repairs the wrong reading.

5. Explain why this refined rule fits this environment.
   Say why this mechanism or interpretation is the right local answer here: cheaper, safer, shallower, clearer, more conservative, easier to prove, or better matched to the surrounding workflow.

6. Land the rule back on the live implementation or exact operational site.
   Name the signal, helper function, API surface, syntax form, command position, or state transition where the rule actually appears.

7. State the guarantee, non-guarantee, and safety boundary.
   Say what this rule now gives the reader, and also what it still does not solve or what outside assumption keeps it safe.

8. Close with a compact final mental model.
   End with the short rule the reader should be able to carry forward and reuse.

The core chain is:
- concrete problem frame and practical use -> simplest idea -> exact breakage -> refined rule -> why it fits here -> exact landing -> guarantee and boundary -> final mental model

For design-heavy notes, this chain should read like one continuous finishing story, not like a tour of finished parts. The preferred feeling is:
- unmet job -> naive build -> visible failure -> minimal fix -> new operating rule -> implementation landing -> final boundary

Do not start by announcing the final block split or final architecture and then unpacking it. Let the split appear as the answer to the failure that came before it.
Use as many `###` beats as needed to keep that growth path visible. More detail is good when it makes the build path, proof boundary, or final split feel inevitable instead of abrupt.

Examples of how this general pattern changes by note type:
- design note: concrete engineering pressure -> simple design -> unfairness or failure -> added mechanism -> why it fits the hardware -> guarantee/non-guarantee -> final shape
- concept note: practical situation -> simple intuition -> hidden exception -> corrected concept -> why that correction matches the real actor model -> scope boundary -> final meaning
- syntax note: practical writing goal -> naive reading of syntax -> ambiguous or wrong behavior -> exact syntax rule -> why the grammar behaves that way -> usage boundary -> final usage rule
- command note: practical diagnostic goal -> obvious command guess -> misleading output or proof gap -> correct workflow step -> why this stage belongs here -> permitted/forbidden conclusion -> final workflow rule

The opening background should usually answer one of these before the local reasoning starts:
- what larger path or subsystem this belongs to
- who reads, writes, drives, or consumes the thing
- what practical task makes the distinction in this note matter
- what resource or latency pressure is shaping the choice
- what kind of mistake a reader would make without this note

## Async-FIFO Pattern

The `venturi/FPGA/async_fifo` family shows a reusable pattern for technical notes that have one governing machine plus several confusing sub-parts.

### Parent Note Pattern: Whole Machine In One Pass

Use this when one note should give the reader the whole mental model before the side stories.

1. Start from the practical job.
   Say what the module is generally used for in direct operational terms.

2. Name the common root.
   Say what the machine essentially is in one sentence.

3. Give the one-pass structure.
   Summarize the whole design in a few high-value bullets or short paragraphs.

4. Turn the summary into a proof contract.
   Make it explicit that the rest of the notes exist to justify the lines of the parent summary. Each child note should exist because one line of the summary needs proof, unpacking, or a boundary explanation.

5. Walk the reader through the pieces in the same order as the summary.
   Give each child link a one-sentence bridge: what local confusion it resolves and why that confusion blocks understanding of the whole machine.

6. Reassemble the machine.
   End the parent note with a compact numbered chain that shows how the pieces fit back together and lets the reader reason forward from operation to operation.

The `async_fifo.md` shape is:
- practical job: move data across unrelated clock domains
- common root: two local pointer islands plus cautious CDC crossing
- one-pass structure: binary local pointers, Gray crossing, `ff_sync`, combinational flags, dual-port memory
- proof contract: "the rest of the notes exist to justify each line of that summary"
- child-note map: pointer width, Gray fullness, CDC synchronizer, `_next` naming, design choices
- reassembly: local pointer -> Gray export -> sync -> compare -> gate operation

A strong parent note often uses this paragraph rhythm:
- one opening paragraph for the practical job and root
- one compact "whole machine in one pass" block
- one "follow the pieces" section where every child link has a reason
- one "assembled picture" section that restores the chain end to end

### Child Note Pattern: Confusion -> Breakage -> Refinement

Use this when a sub-note explains one tricky local point.

1. Start from the wrong or incomplete intuition.
   Example: "Gray is enough", "`_next` means speculative flag", or "full is just pointer equality with wrap".

2. Show where that intuition breaks.
   Name the exact ambiguity, failure mode, or missing bridge.

3. Re-root the explanation in the simpler domain.
   Often this means going back to binary, local state, or the pre-CDC meaning before rebuilding the harder version.

4. Derive the refined rule step by step.
   Do not jump straight to the final formula if the reader needs one intermediate model first.

5. Land the rule back on the live implementation.
   Name the exact signals, helper function, or module boundary where the derived rule appears in the current RTL.

6. Close with the design meaning.
   State what this refined rule buys the design: safety, simpler state, conservative behavior, clearer ownership, easier timing, and so on.

The `async_fifo` child notes repeatedly use this stronger shape:
- `async_fifo_gray_code_fullness.md`: vague full intuition -> binary full meaning -> Gray derivation -> why top two bits flip
- `async_fifo_cdc_synchronizer.md`: Gray is not enough -> metastability still exists -> 2-FF containment -> conservative staleness
- `async_fifo _next state.md`: old `_next` intuition is stale -> new meaning of `_next` -> flags are downstream views of committed state

In practice, many good child notes follow this seven-step teaching loop:

1. Name the pain plainly.
   Use a direct heading or opening line such as "The annoying part" or "Gray is not enough" so the reader knows what confusion is being attacked.

2. Expose the tempting but unsafe shortcut.
   Say the intuition a smart reader is likely to carry in.

3. Retreat to the safest domain.
   Rebuild from binary meaning, local ownership, or committed state before touching the tricky encoding or CDC boundary.

4. Derive instead of quoting.
   Show the intermediate relation that makes the final formula feel earned.

5. Reattach to the current RTL.
   Point to `is_full()`, `ff_sync`, `wr_ptr_gray_next_reg`, or other exact landing sites so the note teaches both concept and code reading.

6. Say what the refinement buys.
   Tie the rule to safety, pessimism, timing, ownership, or clarity.

7. Leave a reusable recall hook when helpful.
   End with a compact checklist, sanity check, or "how I make sure I know this next time" loop if the concept is easy to forget.

### Evolution Pattern: Replace Stale Mental Models

Use this when the current implementation differs from an older common explanation.

1. Name the stale model without apologizing for it.
   Example: the old registered `*_next` flag story or the old inlined synchronizer picture.

2. State what changed in the current RTL.
   Keep the comparison concrete and local.

3. Preserve the root meaning while updating the mechanism.
   Show what stayed conceptually true and what moved structurally.

4. Explain why the new shape is better.
   Prefer reasons such as fewer state variables, clearer ownership, better module boundaries, or easier timing reasoning.

This pattern matters because `async_fifo _next state.md` and `async_fifo_design_choices.md` do not merely explain a design. They also retire old explanations that would now mislead the reader.

## When To Apply Which Pattern

- Use the parent-note pattern when the reader first needs the whole machine.
- Use the child-note pattern when one local confusion would otherwise overload the parent note.
- Use the evolution pattern when older versions or common folklore would give the wrong current mental model.
- Use both together when one system has a clean top-level story but several durable side stories.

## Writing Rules That Matter Here

- Start from use before mechanism.
- Bring in enough background before the mechanism so the reader knows why this local story matters.
- Say what the thing is, not only what it does.
- For durable notes in general, tell the causal learning path, not just the finished abstraction.
- For design-heavy notes, tell the designer's step-by-step finishing path, not only the finished abstraction. A strong story often sounds like: "the pressure here is P, the easy version is X, that breaks in case Y, so the design adds Z, Z fits because of hardware/workflow reason H, and the result guarantees G but still does not guarantee N."
- For concept-heavy notes, use the same root in concept form: "the first practical situation suggests X, that fails because of hidden fact Y, so the real rule is Z, which fits the true actor model because B, and its boundary is C."
- Make each next paragraph earned by the previous one.
- Prefer one governing root over a list of disconnected facts.
- Make child links carry jobs, not only titles. The sentence before the link should say what question the child note resolves.
- Use exact RTL names only after the conceptual bridge exists; then use them as proof anchors.
- Use code fragments only when they prove a local point.
- End by restoring the whole picture so the reader can reason forward from it later.
