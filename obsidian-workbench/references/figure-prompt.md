# Figure Prompt Guide

Use this when the user asks for an image prompt to visualize a concept or relationship.

## Goal

Produce a prompt that someone can hand to an image-generation tool (ChatGPT, DALL-E, Midjourney, etc.) to get a clear technical diagram. The figure should make relationships and structure immediately visible without requiring the viewer to read much text.

## Design principles

- **One core relationship per figure.** Pick the most important structural or causal relationship. Do not try to show everything.
- **Minimal text in the figure.** Labels only — short nouns or short phrases. No sentences inside the diagram.
- **Include supporting concepts** that help the viewer understand the main concept — even if the user did not ask for them. A figure showing only the target concept in isolation is often less clear than one that shows it in context.
- **Use spatial layout to encode meaning.** Hierarchy goes top-to-bottom or left-to-right. Containment shows "is part of." Arrows show flow or dependency. Size difference can suggest capacity or scale.
- **Steps and sequences are welcome.** If the concept involves a process (fetch, translate, evict, unwind), a numbered step flow or a left-to-right timeline makes it clearer than a static box diagram.
- **No decorative elements.** Clean lines, labeled boxes, labeled arrows. Black-and-white or minimal color (one color per category at most).

## What to include in the prompt

1. **Layout description.** Say where each element goes (top, bottom, left, right, inside, beside).
2. **Box labels.** Exact text for each box, including size or capacity where relevant.
3. **Arrow labels.** What each arrow means (fetch, transfer, evict, translate, route, etc.).
4. **Grouping or containment.** Which boxes live inside which (e.g., L1i and L1d are both inside L1 cache).
5. **Supporting concepts.** Name any concept that helps the viewer understand the main one, even if the user did not ask for it. Example: showing DRAM alongside a cache figure makes the cache's purpose self-evident.
6. **What NOT to include.** Explicitly tell the tool to omit decorative elements, gradients, or photorealistic style.
7. **Style line.** End with: "Clean black-and-white technical diagram. Labeled boxes and arrows only. No decorative elements."

## Template

```
Draw a technical diagram showing [main concept] and its relationship to [supporting concepts].

Layout:
- [element A]: [position, size label if relevant]
- [element B]: [position, contained in / beside A]
- [element C]: [position]

Connections:
- Arrow from [X] to [Y] labeled "[what this transfer or relationship means]"
- Arrow from [Y] to [Z] labeled "[...]"

Notes:
- [any grouping, containment, or scale note]
- [any step numbering if sequential]
- No decorative elements. Minimal text. Labels only.

Style: Clean black-and-white technical diagram. Labeled boxes and arrows only.
```

## Example — cache line, L1i, L1d, DRAM

```
Draw a technical diagram showing cache line fetching from DRAM into L1 instruction cache and L1 data cache.

Layout:
- Top: CPU box split into two sub-boxes side by side:
  Left: "L1i — Instruction Cache (32 KB · 512 lines)"
  Right: "L1d — Data Cache (32–48 KB · 512 lines)"
  Both labeled as part of "L1 Cache"
- Bottom: wide box "DRAM" containing a row of equal blocks each labeled "64 bytes"
- Inside each cache box: a few rows of equal-width slots labeled "64 bytes (1 cache line)"

Connections:
- Arrow from DRAM up to L1i labeled "instruction fetch → 64-byte cache line"
- Arrow from DRAM up to L1d labeled "data load/store → 64-byte cache line"
- Note between the two arrows: "independent fetches"

Notes:
- L1i and L1d slots are different shades to show they are separate caches
- Add callout: "cache line size = 64 bytes (same for both)" and "cache total size ≠ cache line size"
- No decorative elements. Labels only.

Style: Clean black-and-white technical diagram. Labeled boxes and arrows only.
```
