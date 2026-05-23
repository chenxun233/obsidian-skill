---
name: obsidian-teaseout
description: "Tease out the core reusable insight from a programming algorithm or code snippet and create a Skill-- note under programming_skill/. Use when: tease out the skill, extract the core logic, what is the real insight here, create a skill note from this code, what makes this work."
---

# Obsidian Tease-Out

Extract the fundamental programming insight from a coding algorithm or solution and crystallize it into a durable `programming_skill/Skill--<name>.md` note in the vault at `/Users/xunchen/Documents/tech`.

## The goal

The goal is NOT to name the surface pattern ("prefix sum + hashmap", "monotonic deque"). The goal is to find the core logical move that makes the solution beautiful — the thing the solution gives you **for free** that the naive approach never gets.

**Example of bad extraction**: "the skill is prefix sum + hashmap."

**Example of good extraction**: "by moving only one pointer `i`, you already have three sums for free: sum(0→i), sum(0→j), and sum(i→j). You never need a second pointer because the difference between any two prefix sums IS the subarray sum. The hashmap just makes the lookup O(1)."

The free lunch is the insight. The data structure is just the container that makes the free lunch cheap to access.

## What to do

### Step 1 — Read the source

Read the referenced vault note, code snippet, or algorithm description. If the user points to a `[[note]]`, read that file. If the user pastes code, analyze it directly.

### Step 2 — Find the naive approach

State explicitly what the brute-force approach would look like and why it is too slow. This is the baseline the insight escapes from.

- What nested loop or repeated scan does the naive solution require?
- What is its time complexity?
- What is the constraint that makes it fail (TLE, N² blowup, etc.)?

### Step 3 — Find the free lunch

This is the core of the skill. Ask these questions in order:

1. **What does this approach give you for free, by construction?**
   - Example: a running prefix sum gives you the sum of any prefix 0→i in O(1), so the difference of two prefix sums gives you any subarray sum without scanning it.
   - Example: a monotonic deque gives you the window maximum in O(1) because dominated candidates are stripped immediately — you never revisit them.

2. **What constraint does this insight eliminate?**
   - Example: "you do not need to move the left pointer to enumerate all subarray sums."
   - Example: "you do not need to re-scan the window for each new position."

3. **What single structure or identity enables the free lunch?**
   - Is it an algebraic identity (prefix sum difference = subarray sum)?
   - Is it a monotone invariant (deque always sorted → front is always the extremum)?
   - Is it a counting trick (frequency map converts O(N) inner scan into O(1) lookup)?

4. **Is the free lunch transferable?** Can you name 3+ other problems where the same insight applies? If yes, the insight is a genuine reusable skill. If you can only name 1 problem, the insight may be too narrow — go deeper until you find a broader principle.

### Step 4 — Name it by the mechanism, not the problem

The name should describe WHAT THE MECHANISM DOES, not the problem it was extracted from.

- Bad name: "subarray sum skill" (names the problem)
- Bad name: "prefix sum" (names the data structure, not the insight)
- Good name: "prefix sum complement lookup" (names the identity + the lookup operation)
- Good name: "monotonic deque" (names the invariant that is maintained)

The name should let a programmer recognize "I have seen this mechanism before" when they encounter a new problem.

### Step 5 — Write the skill note

Create the file at `/Users/xunchen/Documents/tech/programming_skill/Skill--<name>.md`.

The note must follow this structure (look at existing sibling notes in `programming_skill/` for the exact shape):

```
## Recap
- One-line statement of the free lunch (the core insight), in plain English
- The constraint it eliminates ("you do not need a second pointer / inner loop / re-scan")
- Complexity: O(?) time, O(?) space
- When to apply trigger (what problem shape makes this skill the right reach)

<Naming preamble — why the name fits the mechanism>

## Story
### The pressure
<Concrete problem shape + why naive is O(N²) or worse>

### The naive approach
<What the brute force does. Be specific.>

### The free lunch
<State the core insight. Use concrete numbers. Show the three sums, or the eliminated pointer, or the stripped candidates — whatever the mechanism gives for free. This is the heart of the note. Do not rush past it. Make it undeniable.>

### Why the mechanism enables it
<What data structure, invariant, or algebraic identity makes the free lunch O(1) to access? Why is THIS structure the exact right fit?>

### Implementation
<Minimal code showing only the core mechanism, not a full problem solution>

## Variants
<3+ other problems where the same free lunch applies. State what the "prefix value" or "monotone quantity" is in each variant.>

## Common Trap
<What does a programmer do when they MISS the insight? They fall back to a nested loop or second pointer. Call that out explicitly.>

## Final mental model
<One paragraph. State the free lunch, the constraint it eliminates, and the structure that makes it O(1). Should be memorable enough to reconstruct the technique from scratch after reading once.>
```

### Step 6 — Wire links

- Wire outgoing wikilinks to any vault notes the skill note references (the source problem note, related container notes, variant problem notes).
- Add a reverse link back INTO the source note (the coding-test note or wherever the algorithm lives). Add it at a natural anchor — typically the "Reusable techniques" section.
- Search the vault for other notes that use the same mechanism without linking to this skill note; add strong incoming links where they belong.

### Step 7 — Log creation

Append one creation line to `Wiki Ops/logs/YYYY-MM/YYYY-MM-DD.md`. Read the file first. Append only — never overwrite.

## Non-negotiable rules

- **The free lunch must be stated in plain English before any code appears.** A reader who only reads the Recap and the first paragraph of the Story should understand the core insight without reading a single line of code.
- **Name the constraint that is eliminated.** "You do not need X" is the most powerful sentence in the note. Find it.
- **Use concrete numbers to show the free lunch.** Abstract claims are hard to remember. "By moving one pointer i, you already have sum(0→i)={6}, sum(0→j)={13}, and sum(i→j)={7} for free" is unforgettable. "Prefix sums let you compute subarray sums" is not.
- **The free lunch must transfer to 3+ problems.** If it does not, the extraction is too narrow. Go deeper.
- **Do not duplicate the source problem note.** The skill note captures the MECHANISM. The problem note captures the PROBLEM. They are linked but do not repeat each other's content.
- **No backtick-wrapped wikilinks.** Vault notes on linked concepts must use `[[...]]`, never `` `[[...]]` ``.
- **Do not self-link.** Use **bold** for the note's own name in its own prose.

## Self-review before finishing

Run these three checks explicitly before declaring the note done:

1. **Truth**: Is the free lunch claim correct? Can you verify it with a 3-element example?
2. **Transferability**: Are the 3+ variants real? Does the same core mechanism apply in each?
3. **Plain-English first**: Can a junior programmer read the Recap and first Story paragraph and state the insight back in their own words without reading the code?
