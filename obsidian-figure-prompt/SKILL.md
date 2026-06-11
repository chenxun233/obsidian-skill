---
name: obsidian-figure-prompt
description: "Generate a paste-ready image prompt for visualizing a concept, relationship, or process. Use when: draw a figure, visualize this concept, make a diagram, image prompt, ChatGPT draw, illustrate relationship."
---

# Figure Prompt

Generate a self-contained prompt the user can paste directly into an image-generation tool (ChatGPT, DALL-E, Midjourney, etc.) to get a clear technical diagram.

## Purpose

Figures are created for **understanding the mechanism at a single glance** — not for showing detail. A good figure lets a reader instantly grasp the core relationship, flow, or structure without reading any prose. If a figure requires the reader to study it for more than a few seconds, it has too much detail. Strip everything down to the essential actors, one or two key relationships, and the governing rule. Detail belongs in the note text, not the figure.

## What to do

1. Read `references/figure-prompt.md` for design principles and the prompt template.
2. **If the concept has a vault note, read it before writing the prompt.** Do not reconstruct sequence or containment relationships from memory — read the note and copy the exact causal order and hierarchy from it. A function that contains internal logic must be drawn as a container box enclosing that logic, not as a peer step before it.
3. Identify the main concept the user wants visualized.
4. Identify supporting concepts that help understanding — include them even if the user did not ask, as long as they make the figure clearer.
5. **Pick the matching style** before writing the prompt. An algorithm trace over a data structure (linked list, array, stack, tree walk, sort pass, search step) uses the [Algorithm walkthrough style](#algorithm-walkthrough-style-hello-algo). A system or mechanism diagram (network pipeline, kernel path, scheduling flow) uses the [Lean style](#lean-style-preferred). A single static concept (containment hierarchy, taxonomy) uses Lean style without step numbering.
6. **Ruthlessly cut detail.** If an element does not directly serve the one-glance insight, remove it. Prefer fewer, larger, clearer elements over many small ones.
7. Produce only the prompt itself — no explanation, no preamble. The output should be something the user can copy and paste immediately.

## Notation convention for indexed data structures

When a figure involves arrays, hash maps, or any indexed data structure, use this notation consistently throughout the entire prompt and the resulting diagram:

- **`[N]`** — an **index** (a position in a sequence). Use for array subscripts and index labels. Example: `[0]`, `[3]`, `[i]`.
- **`{V}`** — an **element** (a stored value, a hash key, or any data value). Use for element contents and hash-map keys. Example: `{7}`, `{target}`, `{nums[i]}`.

**Never use `[V]` to label a value.** The bracket form `[...]` is reserved exclusively for positions. A hash-map lookup on value 7 is written `seen{7}`, not `seen[7]`, because 7 is a value being used as a key, not an index.

**Never write accidental double brackets `[[...]]`.** Double brackets arise when individual index brackets `[N]` are accidentally nested inside a list bracket. Use exactly one bracket pair in each context:

| Situation | ✗ Wrong | ✓ Correct |
|---|---|---|
| List of indices as a hash-map value | `[[0], [3]]` | `[0, 3]` |
| Single index standalone (subscript, pointer) | — | `[0]` |
| Emitted index pair | `[[0], [1]]` | `([0], [1])` |
| Hash-map key (a value, not an index) | `seen[7]` | `seen{7}` |

**Exception — genuine array-of-arrays:** when the data structure itself holds sub-arrays as elements (2D arrays, adjacency lists, list-of-intervals), double brackets are correct and expected. `[[1, 2], [3, 4]]` is right because each inner `[...]` is an array element, not an index label. The ban applies only when `[[...]]` arises from accidentally wrapping an index `[N]` inside a list bracket.

**Self-check before finalising any prompt:** scan the prompt text for `[[`. Ask: does each instance represent a genuine array-of-arrays element, or is it an accidentally nested index label? Fix the latter; keep the former.

Apply this notation to every label in the figure: array box contents, hash-map key labels, complement calculations, pointer annotations, and caption text. Inconsistent notation defeats the purpose of the convention and confuses the reader.

## Hash tables, bucket arrays, and chained structures

The governing requirement is **arrow correctness: every arrow must visibly start at its exact source and end on its exact target node.** In a bucket-array-with-chains figure the usual failure is an arrow that floats or lands ambiguously — a slot's chain that does not visibly connect back to that slot. The layout below makes the alignment automatic; the layout is only a means, arrow correctness is the end.

- **Draw the bucket / index array as a VERTICAL column** of slots (`[0]` at top, then `[1]`, `[2]`, … downward).
- **Each slot's chain extends HORIZONTALLY to the RIGHT, on that slot's own row**, so `[1] → {1} → {5}` is one straight line beginning at slot `[1]`. The node then sits on the same row as the slot that points to it, so the arrow's two endpoints are unambiguous.
- A **horizontal row of slots** forces the chained nodes to float off to the side, unaligned with their slot — arrows then land ambiguously. Do not use it.
- **Empty slots:** a small gray slot box with no chain.

For a **before → after transformation** (rehash, resize, grow ×2):

- Draw **each state as its own self-contained, correctly-wired snapshot** (vertical array + per-row chains) so every arrow inside it connects to the right node. The two states may be **stacked or placed side by side — the layout does not matter; only the arrow correctness within each state does.**
- **Do NOT route both states' arrows into one shared central node band** — shared-band arrows lose their targets and the second array reads as disconnected.
- To show the elements **do not move** (node-based storage), draw ONE labeled dashed *identity tie* from a single exemplar node in the Before state to the same node in the After state (e.g. `{1}` to `{1}`, "same node · address unchanged").

Validated empirically (the `unordered_map` rehash figure): the failure was always a **misplaced arrow** — a vertical array with per-row chains fixes it; a horizontal slot row or a shared node band leaves arrows landing in the wrong place.

## One container = one box (multi-element rendering)

A single container that holds several elements must be drawn as **ONE box with the elements comma-separated inside it** — never as several adjacent single-element boxes. Splitting one container into per-element boxes teaches the false mental model that each element is its own separate container.

This bug is most common in adjacency lists, hash-map buckets, and any "index → list of values" structure. When a node `0` points to neighbors `1` and `2`, the inner vector `adj[0]` holds both, so it is **one** box:

| Situation | ✗ Wrong (splits one container) | ✓ Correct (one box) |
|---|---|---|
| Inner vector with two ints | `{ 1 }` `{ 2 }` | `{ 1, 2 }` |
| Inner vector of two pairs | `{ 1, 5 }` `{ 2, 3 }` | `{ {1, 5}, {2, 3} }` |
| Hash-map bucket, two strings | `{ "B" }` `{ "C" }` | `{ "B", "C" }` |

**Always state the rendering rule explicitly in the prompt** whenever the figure shows a container holding more than one element, e.g.: "each index slot points to exactly ONE box; multiple elements are listed comma-separated inside that single box, NOT as separate boxes." Image models default to one-box-per-token unless told otherwise.

**Distinguish from genuine multi-slot structures.** Separate boxes ARE correct when each box is its own indexed slot of the OUTER container (e.g. the array cells `[0] [1] [2]` of a `vector`, or successive nodes of a linked list). The one-box rule applies only to the elements held INSIDE a single container slot — the inner list, the bucket, the row. Outer slots: many boxes. Inner contents of one slot: one box.

**Self-check before finalising:** for every container in the prompt, ask "is this drawn as one box, or did I accidentally split its elements into separate boxes?" Collapse any split inner container back into a single comma-separated box.

**`unordered_map` iteration-order disclaimer.** Whenever a figure shows the internal state of a `std::unordered_map` (or any hash table) evolving across steps, add a small italic label on the map-state column header:

> *Entries shown sorted by key for readability — actual `unordered_map` iteration order is undefined and is NOT insertion order.*

Place it as a one-line annotation directly below the column header, in light gray italic text. This prevents the figure from teaching the false mental model that hash maps preserve insertion order. Do not omit this disclaimer even when the shown order happens to match insertion order in the example — the coincidence is misleading.

## Delta highlighting in multi-step figures

Any figure that shows state evolving across multiple steps (algorithm traces, sorting passes, pointer sweeps, graph traversals, state machines, protocol exchanges) must make it immediately obvious what changed in each step — without the reader having to mentally diff two rows.

- **Highlight new or changed elements** in each step using a bolder border, a distinct tint, or a `★ NEW` badge. Leave carry-over elements at normal weight.
- **Fade or gray out** elements that were active in a previous step but are no longer relevant now.
- The rule: a reader scanning any single row must be able to identify the delta in under one second, without looking at adjacent rows.

This applies to every evolving-state figure: a pointer moving across an array, a new node inserted into a tree, a new entry added to a map, a queue gaining or losing an element, a variable being updated. The delta is the lesson — make it the most visually prominent thing in the row.

## Arrow disambiguation in multi-role figures

When a figure uses arrows with more than one meaning (e.g. "maps to" inside a data structure, "emits" in a flow, "points to" in a pointer diagram, "causes" in a causal chain), assign a distinct visual style to each role and include a one-line legend:

- **Solid arrow →** : flow or sequence ("next step", "calls", "sends to")
- **Dashed arrow -->** : reference or lookup ("points at", "reads from", "maps to")
- **Double arrow ⟹** : produces or emits ("outputs", "yields", "emits pair")

Not every figure needs all three. Use only the styles that actually appear, and list them in a small legend box in a corner of the figure. The goal is that the reader never has to guess what an arrow means.

## Output shape

- **Default orientation: horizontal (left to right).** All main flows, pipelines, and sequences run left to right unless the user explicitly requests vertical or the concept is inherently top-to-bottom (e.g. a call stack, a memory layout). Always state "flow runs left to right" explicitly in the prompt so the image generator does not default to vertical.
- **Multi-gate / multi-stage pipelines**: place all gates or stages in a single horizontal row connected by short arrows. Rejection or hold branches drop downward below the main pipeline row — they never become separate horizontal swim lanes. The happy path (NO / pass) always continues rightward along the top row; the rejection path (YES / fail) always drops down from the gate diamond. This keeps the diagram compact and the flow direction obvious.
- Layout description (where each element goes)
- Box labels with size/capacity where relevant
- Arrow labels (what each connection means)
- Grouping or containment notes
- Step numbering if the concept is a process or sequence
- End with a style line. Use color when it makes structure or category distinctions clearer — one color per distinct category. If color helps, end with: "Clean technical diagram. Labeled boxes and arrows only. Use color only where it aids understanding — one color per category. No decorative elements." If color would not add meaning, use the black-and-white variant instead.

## Shape rule

If an actor or component is a recognizable real-world object, describe it in its natural shape rather than a plain rectangle. Examples: a server → draw as a server rack or tower; a router → draw as a router/switch device with port indicators; a client or user machine → draw as a laptop or desktop computer; a database → draw as a cylinder; a phone → draw as a smartphone outline. Reserve plain labeled rectangles for abstract concepts (queues, buffers, state machines, protocols) that have no obvious real-world shape.

**Critical**: applying real shapes means substituting the icon only. The layout, section structure, hierarchy, swim lanes, arrow directions, groupings, and all relationships must remain exactly as described in the prompt. Do not redesign or restructure the diagram to accommodate the new shapes — place the real-shape icon exactly where the plain rectangle would have been.

**Actor ownership rule**: any processing box, computation label, or internal state annotation (e.g. "tcp_ack() → cwnd reduced", "queue building", "state machine") must be placed physically on or immediately beside the actor that performs that processing — not floating in the middle between two actors. Ambiguous center placement implies the processing happens between actors, which is almost always wrong. If an actor on the right performs the computation, the box goes on the right side next to that actor's icon.

**No duplicate icons across stages**: an artifact created in one stage (e.g. a cylinder representing a file descriptor, a box representing a handle) must be drawn exactly once, in the stage where it is created. Later stages that use that artifact must receive it via a crossing arrow from the originating stage — never by redrawing the same icon. A second copy of the same icon implies a second creation, which is wrong.

**Variable name consistency**: use the same name for the same artifact everywhere in the diagram. If a cylinder is labeled `epoll_fd` in Stage 1, every function call in every later stage that takes that fd as an argument must also spell it `epoll_fd` — not an alias like `epfd`. Inconsistent naming implies different variables, which confuses the reader.

**Annotation boxes vs flow branches**: a stage-level property or invariant (e.g. "watch set persists across calls", "no rebuild") is not a flow branch. Place it as a standalone floating annotation box inside the stage region with no arrow connecting it to any decision diamond. Only actual control-flow outcomes (retry, dispatch, error) get arrows out of a diamond. Mixing annotations into the branch arrows makes the diagram look like more exit paths exist than actually do.

## Lean style (preferred)

Apply this style by default unless the user asks for a different style.

**Text budget: 2–4 words per label.** Arrow labels, box labels, and annotations must all be 2–4 words maximum. Never a full sentence. Never an explanation inside the diagram. If something needs a sentence to explain, it belongs in the note text, not the figure.

**Color carries meaning, not decoration.** Assign one color per category and use it consistently. Examples: green = active data path or healthy state; red/orange = error or danger; blue = neutral/background mechanism; magenta/pink = operation call or trigger. Do not assign a second color to the same category and do not add colors just because a box is large.

**No floating description boxes.** Never draw a box that contains a full sentence or a multi-word explanation of what is happening. If a region needs a label, use a 1–3 word title at the top of the region, not a paragraph inside it.

**Let geometry encode relationships.** Use containment (one box inside another) to show ownership. Use adjacency (side by side with a short arrow) to show sequence. Use vertical position (below) to show failure or error branches. Do not add a sentence label when the position already says the same thing.

**Annotations below the diagram: 3–5 words max.** If a short caption is needed below the whole figure, keep it to one 3–5 word phrase. No paragraph, no bullet list below the diagram.

**Icons over rectangles for real objects.** Use recognizable icons for hardware (NIC, server chassis, computer, phone). Use cylinders for buffers or FDs. Reserve plain rectangles for abstract concepts only.

**Short signal/variable names on arrows.** Prefer names already in the code (e.g. EAGAIN, n, FIN, EPOLLET) over prose descriptions. An arrow labeled "EAGAIN" is clearer and shorter than "buffer empty signal returned".

## Algorithm walkthrough style (hello-algo)

Use this style when the figure shows an algorithm running step by step over a concrete data structure (linked list, array, stack, queue, tree, heap, sorted bars). Modelled on the figures in [hello-algo.com](https://www.hello-algo.com/) — clean, airy, one teaching beat per image.

**One composite figure with stacked step rows.** A multi-step trace produces ONE prompt that yields ONE image containing all steps stacked vertically. Do not emit a series of per-step prompts. The reader scans the whole algorithm in one place; the steps share a consistent color legend and visual rhythm down the column, which is the actual teaching benefit.

**Composite layout signature.** The single image is a portrait-ish canvas (taller than wide is fine — let the height grow with the number of steps), pure white background, with this fixed structure:

- A short title strip at the very top — bold dark-gray text naming the algorithm and the example input (e.g. "Remove duplicates from sorted linked list — trace on 1→2→2→2→3→4→4→5"). One line only.
- Below the title, a vertical stack of step rows. Each row is one horizontal band across the full canvas width.
- Inside a row: on the far left, a light-gray rounded-rectangle `Step N` badge with dark-gray text. To its right, the diagram for that step (the linked list / array / data structure at this step). To the right of the diagram (or directly below it if the row is wide), a light-gray rounded-rectangle caption box with one short declarative sentence describing what this step does.
- Between rows, a thin horizontal light-gray separator line, or just generous vertical whitespace — enough that each row reads as its own beat without scrolling the eye.
- A small `www.hello-algo.com`-style watermark or attribution can be omitted; if added, place it bottom-right in light-gray small text.
- For steps that contain a splice/insert sub-sequence (before → code rewrite → after), keep that mini before/after inside the row by stacking two sub-frames within the row with a short downward gray arrow between them whose label is the literal code rewrite. The row is still one row in the composite — just slightly taller than an advance-only row.

**Three-tone color system, used consistently across the whole series.** Assign roles once and never reassign:

- **Brand green** (#5FB28F-ish) = data values; node fill for linked-list nodes; bar fill for active-range array elements. Numeric labels above bars or inside nodes use the same green.
- **Blue** = boundary or persistent pointer (i, j, head, P, prev). Caret marker, letter label, and any highlight rectangle border for that pointer's element all share the blue.
- **Orange** = dynamic, newly-computed, or newly-created pointer (m for midpoint, P for a node being inserted). Same caret + letter + border treatment as blue, just in orange.
- **Gray** = inactive, faded, out-of-range, or spliced-out elements. Fill and border both gray. Old arrows leading to a spliced node become dashed gray.

Reuse the exact same color-to-role mapping on every figure in the series, so the reader learns the legend once.

**Pointer marker convention.** A pointer is *not* drawn as a labeled arrow shooting into the node. Instead: place a small caret `^` directly under the index tick (for arrays) or under the node (for linked lists), and place the pointer letter (`i`, `j`, `m`, `P`, `n0`, `n1`) under the caret in the matching color. This keeps the diagram horizontal-thin and never overlaps the data row.

**Active element highlight.** Wrap the active node/bar in a hollow thick-bordered rectangle whose border color matches the owning pointer. The fill stays the data color (green); only the border changes. Do not flood-fill an active element.

**Transitions inside a single figure** (only when the step inherently contains a small before → after micro-sequence, like inserting a node which is two pointer rewrites). Stack mini-snapshots vertically. Between them, draw a short downward gray arrow whose label is the literal code statement of the rewrite (e.g. `P.next = n1`, `n0.next = P`, `cur->next = cur->next->next`) and place a parenthetical English gloss below: `(Set P point to n1)`. Code identifiers in the label keep their assigned colors (P orange, n0/n1 blue). Prose lives only in the parenthetical, never in the arrow label itself.

**Null terminus.** The end of a list, an empty pointer, or a sentinel is the word `None` in light gray text — not a box, not `∅`, not `nullptr`. Place it where the next node would be, slightly offset to the right with a short arrow leading to it from the last real node.

**Faded / spliced-out / deleted elements.** Re-render the same shape but with gray fill, gray border, dashed outline. The arrow that used to point at it becomes dashed gray. Do NOT overlay a red X. Hello-algo's deletion figure proves this: the ghost of the deleted node remains visible in gray to show what the pointer rewrite removed, with a caption that explains "we consider the node to have been deleted."

**Variant family figures** (e.g. singly / doubly / circular linked list shown side-by-side as conceptual peers, not algorithm steps). Stack three rows vertically. Above each row, a bold green section title (`Singly linked list`, `Circular linked list`, `Doubly linked list`). Each row shows the same five-node example so the structural difference is the only thing that varies between rows. No step badge here — this is a single-concept reference figure, not a trace.

**Captions: code-colored identifiers in prose.** Inside the gray caption box (and any explanatory annotation in the figure), render variable names in their assigned color: `i` blue, `j` blue, `m` orange, `P` orange, `n0` green. The reader's eye locks the same color to the same role across all eight steps.

**Caption shape.** One declarative sentence is the default. If the step performs a literal code computation, write the caption as a short numbered list — typically two lines: `1. Calculate the midpoint m = (i + j) / 2` followed by `2. ∵ nums[m] == target ∴ Return index m`. Keep these to two or three lines max; if the step needs more explanation, split it into two figures.

**Whitespace and aspect.** Targets: 16:9 canvas, diagram occupies ~55% of the area centered, caption box ~20% below it, the rest is breathing room. Resist the urge to fill the whitespace — it is the point. Crowded diagrams stop reading as algorithm walkthroughs and start reading as architecture diagrams.

**Style line to append to the composite prompt:**

> Clean technical diagram in the hello-algo.com style. White background, portrait canvas tall enough to fit all step rows comfortably. One short title strip at the top; below it, a vertical stack of step rows, each row containing a `Step N` badge on the left, the diagram in the middle, and a one-sentence light-gray caption box on the right or directly below. Brand green for data values and node fills; blue for boundary pointers (i, j, head, cur); orange for dynamic/computed pointers (m, next, inserted node); gray for inactive/spliced/out-of-range elements. Pointer markers as caret `^` under the index/node with the letter below in matching color. Active element shown as hollow thick-bordered rectangle around the data shape, fill unchanged. Null terminus as the word `None` in light gray. Spliced-out elements drawn as a faded gray dashed ghost — no red X. Generous whitespace between rows. No decorative elements.
