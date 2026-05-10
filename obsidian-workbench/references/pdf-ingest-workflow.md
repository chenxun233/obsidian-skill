# PDF Ingest Workflow

Use this when learning-checklist ingest or durable note work depends on a PDF source.

This workflow absorbs the useful part of the old `pdf` and `pdf-reading` skills into `obsidian-workbench`, with emphasis on source understanding rather than PDF creation.

## Root Rule

- Do not trust raw text extraction alone when layout, figures, or scans matter.
- First identify what kind of PDF you have.
- Then choose the cheapest reading method that still preserves the evidence you need.

## Step 1: Inventory The PDF

Run a quick diagnostic first:

```bash
pdfinfo document.pdf
pdftotext -f 1 -l 1 document.pdf - | head -20
pdfimages -list document.pdf
pdfdetach -list document.pdf
pdffonts document.pdf
```

This tells you:
- page count and job size
- whether text is extractable or the file is effectively scanned
- whether images or figures are embedded
- whether attachments exist
- whether font issues may break text extraction

## Step 2: Choose The Reading Strategy

- Text-heavy PDF:
  use text extraction first; rasterize only the pages whose layout or figures matter
- Scanned PDF:
  rasterize pages and inspect visually; use OCR only if bulk text is necessary
- Slide-deck PDF:
  treat pages as visual first; rasterize on demand
- Figure- or table-heavy PDF:
  combine text extraction with page rasterization
- Form-heavy PDF:
  extract fields if needed, then rasterize for visual context

## Step 3: Extract The Right Evidence

### Text extraction

Use `pdftotext -layout` or `pdfplumber` when content is primarily textual.

### Visual inspection

Rasterize only the pages that matter:

```bash
pdftoppm -jpeg -r 150 -f 3 -l 3 document.pdf /tmp/page
ls /tmp/page-*.jpg
```

Use rendered pages when charts, equations, page layout, or figure meaning matters.

### Embedded images

```bash
pdfimages -png document.pdf /tmp/img
```

Remember: vector-drawn charts may not appear here. For those, rasterize the whole page instead.

### Attachments

```bash
pdfdetach -list document.pdf
pdfdetach -saveall -o /tmp/attachments/ document.pdf
```

If the PDF contains spreadsheets or source files, ingest may need those too.

## Step 4: Persist For Obsidian Work

- For learning checklist ingest:
  extract only the evidence needed to build the checklist path
- For durable notes:
  cite the PDF-derived mechanism, figure, or wording only where it changes the note's logic
- For both:
  keep the source boundary visible, especially when the PDF is visual and text extraction is incomplete

## Practical Boundary

- Use text extraction for searchable content.
- Use rasterization for layout truth.
- Use both when precision matters.
- Do not summarize a PDF confidently until you know whether the important meaning lives in text, layout, figures, or attachments.

## Non-Goals

This workflow is for reading and ingest support.

It is not the place for:
- PDF creation
- form filling
- merging or splitting PDFs
- watermarking
- encryption
