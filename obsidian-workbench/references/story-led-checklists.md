# Story-Led Checklist Rules

Use this reference when a checklist should teach through story instead of behaving like a detached checkbox list.

## Story Order
- The story order must be visible and justified.
- Default to one of:
  - logic sequence
  - time sequence
  - easy-to-hard teaching sequence
- If the reader cannot tell why one section comes before the next, rewrite the order.

## Checkpoint Landing
- Every checkpoint must link directly to at least one reusable note.
- When the landing target is a reusable kernel function or similar API, use a plain wikilink such as `[[lock_sock()]]`; never wrap the wikilink in backticks.
- Because direct landing is required in checklists, a checkpoint may link to a downstream note even when a nearby higher-level recipe already exists.
- Outside that requirement, avoid duplicate link fanout. Do not repeat sibling or child recipe links when the local checkpoint does not need direct landing on them.

## Interleaving
- Keep the main path as a story with inline checkboxes at turning points.
- Do not write the story first and then dump leftover sibling checks under it.
- Every checkpoint should arrive exactly where the story now needs that skill, proof, or note.
- If a paragraph is followed by a bundle of checkpoints without a clear local "why now?" bridge for each one, rewrite the section.

## One Checkpoint As Default Unit
- Treat one checkpoint as the default unit of landing.
- Keep multiple sibling checkboxes together only when they answer one immediate question, share the same local bridge, and would become more confusing if separated.

## Local Evidence And Boundary
- Each checkpoint should preserve or later gather:
  - reusable note home
  - evidence, command, example, or mastery check
  - proof standard and boundary when that distinction matters
  - carry-forward application for next time

## Procedure And Recipe Boundary
- Do not promote every branch into a Recipe.
- Create or revise a Recipe only when the branch owns a strong reusable procedure with stable next-time steps, evidence shape, and boundary.
- If the branch is mainly a caution, weakening result, proof boundary, or case-shaped observation, keep it in the story, checklist, Deep note, or raw issue record.

## Proof Ladder
- For diagnostic or procedural checkpoints, make the ladder explicit before the learner runs commands:
  - previous proof -> current proof -> next proof
- State what the current evidence permits, forbids, and what to fix if the stage fails.
