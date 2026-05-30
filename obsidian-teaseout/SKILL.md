---
name: obsidian-teaseout
description: "Process a LeetCode problem into three artifacts: the problem note (instance + solution), pattern notes (recipes), and primitive notes (intent-to-code translation units). Deduplicate aggressively; reuse beats create. Use when: tease out this problem, add this problem to vault, extract pattern and primitives."
---

# Obsidian Tease-Out

Given a LeetCode problem, produce a minimal set of vault notes:
1. **One problem note** at `Leet Code/LC <index>--<name>.md`.
2. **Zero or one pattern note** at `coding skill/patterns/Pattern--<name>.md`.
3. **Zero or more primitive notes** at `coding skill/primitives/Primitive--<name>.md`.

**Default behavior is REUSE, not CREATE.** A well-functioning vault should add zero or one new pattern/primitive notes per problem. Only create a new pattern or primitive when no existing one fits.

## The architecture

- **Problem note** = the instance. Holds the problem statement, the specific solution, full code. Links out to its pattern and primitives.
- **Pattern note** = the recipe. Names the algorithmic shape. Lists composing primitives as wikilinks. No full solution code.
- **Primitive note** = the intent-to-code unit. Names a single task a programmer can state in plain English ("I want to…") but does not yet know how to express in code. Holds the minimal C++ idiom that realizes that intent. Reusable across patterns. No full solution code.

The problem note is a junction box. The pattern and primitive notes are the permanent vocabulary.

## What to do

### Step 1 — Read the source

Read the problem statement and the user's solution / approach. If the user describes what they knew vs. didn't know, treat the "didn't know" parts as candidate primitive gaps.

### Step 2 — Identify the pattern

Name the pattern in 3–7 words. Examples: "Grid BFS", "Sliding window with counter", "Monotonic stack — next greater", "DP on intervals", "Union-find".

**Then check for existence:**
- List `coding skill/patterns/` with `ls`.
- If a `Pattern--<name>` note with a matching name exists, **reuse it**. Do not create.
- If a near-match exists (e.g., this is "Grid BFS" and "Grid BFS" exists), **always reuse**. Variation goes into primitives, not new patterns.
- Only create a new `Pattern--` note if no existing pattern covers this problem's shape.

### Step 3 — Identify the primitives

List every place in the solution where a programmer would know *what* they want to achieve but not yet *how* to code it. Aim for 3–6. For each, write the **gap** as a plain-English intent statement: *"I want to X"* — the exact sentence a stuck programmer would say before knowing the idiom.

Examples of primitive gaps:
- "I want to avoid revisiting cells."
- "I want to process BFS nodes one layer at a time."
- "I want to signal that no answer was found."
- "I want to compute the width of the popped span on a monotonic stack."

The gap is indexed by **intent, not by mechanic**. If two problems share the same intent, they share the same primitive — even when the exact C++ idiom differs slightly. Different idioms become Variants.

**Then check for existence:**
- List `coding skill/primitives/` with `ls`.
- For each primitive candidate, grep existing `Primitive--*.md` files for the `Gap:` line.
- If an existing primitive covers the same intent, **reuse it**. If this problem uses a *new idiom for the same intent*, **edit the existing note's Variants section** — do not create a new primitive.
- Only create a new `Primitive--` note if the intent is genuinely new.

### Step 4 — Write the problem note

Create `Leet Code/LC <index>--<name>.md`:

```
## Problem
<1–2 sentence restatement, stripped of LeetCode flavor>

Constraints: <key bounds, e.g., n ≤ 10^5>

## Pattern
[[Pattern--<name>]]

## Primitives used
- [[Primitive--<name1>]] — <one-line note of how it applies here>
- [[Primitive--<name2>]] — <one-line note of how it applies here>
- ...

## Solution
```cpp
<full working C++ solution>
```

## Stall points I hit
- <verbatim "I didn't know how to..." question, if any>
- <the primitive that filled it>

## Complexity
- Time: O(?)
- Space: O(?)
```

### Step 5 — Write or update the pattern note

If creating a new `Pattern--<name>.md`:

```
## Signal
"<phrases in problem statements that trigger this pattern>"

## Composed of
- [[Primitive--<name1>]]
- [[Primitive--<name2>]]
- ...

## Skeleton
<4–7 step English skeleton, no syntax. The pattern's canonical shape.>

## Problems
- [[LC <index>--<name>]]
```

If the pattern already exists, only update its `## Problems` section to include this LC link.

**Hard cap: 20 lines.** A pattern note is a recipe card, not a tutorial. The primitives carry the detail.

### Step 6 — Write or update primitive notes

If creating a new `Primitive--<name>.md`:

```
## Gap
"I want to <plain-English intent — the exact sentence a stuck programmer would say>"

- <bullet: when this primitive is the right reach>
- <bullet: when a related but different structure is better — same space-for-time idea, different tool>
- <bullet: when NOT applicable — what problem shape disqualifies it>

## Move
<1–3 lines of concrete C++ idiom that realizes the intent — the default approach>

## Variants
- <variant 1: alternative idiom for the same intent>
- <variant 2: ...>

## Trap
<the specific bug that occurs when this primitive is done wrong>

## Used in
- [[LC <index>--<name>]]
```

If the primitive already exists:
- Add this LC to `## Used in`.
- If this problem demonstrated a *new idiom for the same intent*, add it to `## Variants`.
- Do not touch other sections.

**Hard cap: 15 lines.** Scannable in 30 seconds.

### Step 7 — Verify links

After writing all notes:
- Every wikilink resolves to an existing file.
- The problem note's `Pattern` and `Primitives used` links match what was created/reused.
- The pattern note's `Problems` section includes this LC.
- Each primitive note's `Used in` section includes this LC.

### Step 8 — Log creation

Append one line to `Wiki Ops/logs/YYYY-MM/YYYY-MM-DD.md` summarizing: which problem was added, which pattern (new or reused), which primitives (new, reused, or updated-with-variant).

## Non-negotiable rules

- **REUSE BEATS CREATE.** Before creating any pattern or primitive note, prove the existing vault doesn't already have it. A typical problem produces 1 new problem note + 0 new patterns + 0–1 new primitives.
- **Primitives are indexed by INTENT, not by idiom.** Same "I want to…" intent → same primitive, even if the C++ idioms differ. Multiple idioms become Variants.
- **Pattern notes never contain full problem solutions.** Only skeletons.
- **Primitive notes never contain full problem solutions.** Only the mechanic snippet.
- **All links are wikilinks, never backtick-wrapped.**
- **The problem note links out; pattern and primitive notes link back.** Bidirectional, always.
- **Length caps are real:** problem note ~60 lines, pattern ~20, primitive ~15.

## Self-review before finishing

1. **Deduplication check:** Did I `ls` both directories and grep existing `Gap:` lines before creating? If I created a new primitive, can I state the "I want to…" intent and confirm no existing primitive covers it?
2. **Granularity check:** Is each primitive small enough that it's reused across multiple patterns? If it's only ever used in one pattern, the intent may be too problem-specific — broaden it or fold it into the pattern note.
3. **Link check:** Does every wikilink resolve? Does every back-link exist?
4. **Length check:** Is each note under its cap?
