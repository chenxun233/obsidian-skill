---
name: figure-prompt
description: "Generate a paste-ready image prompt for visualizing a concept, relationship, or process. Use when: draw a figure, visualize this concept, make a diagram, image prompt, ChatGPT draw, illustrate relationship."
---

# Figure Prompt

Generate a self-contained prompt the user can paste directly into an image-generation tool (ChatGPT, DALL-E, Midjourney, etc.) to get a clear technical diagram.

## What to do

1. Read `references/figure-prompt.md` for design principles and the prompt template.
2. Identify the main concept the user wants visualized.
3. Identify supporting concepts that help understanding — include them even if the user did not ask, as long as they make the figure clearer.
4. Produce only the prompt itself — no explanation, no preamble. The output should be something the user can copy and paste immediately.

## Output shape

- Layout description (where each element goes)
- Box labels with size/capacity where relevant
- Arrow labels (what each connection means)
- Grouping or containment notes
- Step numbering if the concept is a process or sequence
- End with the style line: "Clean black-and-white technical diagram. Labeled boxes and arrows only. No decorative elements."
