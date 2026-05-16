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
5. **Ruthlessly cut detail.** If an element does not directly serve the one-glance insight, remove it. Prefer fewer, larger, clearer elements over many small ones.
6. Produce only the prompt itself — no explanation, no preamble. The output should be something the user can copy and paste immediately.

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
