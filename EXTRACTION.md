# Extraction Rules

Detailed rules for extracting figures, tables, and equations from paper sources.

## Figures

- Export all body figures to `assets/figure-NN.png` (e.g., `figure-01.png`, `figure-02.png`)
- Reference with relative paths in Markdown
- Place figures near their original position, adjacent to their caption
- If a figure cannot be individually extracted, crop a readable region from the rendered page — never silently omit

### PDF Extraction Strategy

Prefer page-area rendering over raw image object export:

```python
import fitz  # PyMuPDF

doc = fitz.open("paper.pdf")
page = doc[page_number]

# Define the figure bounding box (x0, y0, x1, y1)
clip = fitz.Rect(x0, y0, x1, y1)

# Render at 2x resolution with white background (alpha=False prevents black backgrounds)
mat = fitz.Matrix(2, 2)
pix = page.get_pixmap(matrix=mat, clip=clip, alpha=False)
pix.save("assets/figure-01.png")
```

**Only use raw image export** (`page.get_images()`) when the image object exactly matches the rendered result — no soft masks, transparency, overlaid text, vector annotations, or multi-layer compositing.

### Multi-column PDFs

- Identify which column contains the figure and its caption
- Clip to that column's boundaries — do not extend across the full page width
- Allow minimal margin, but exclude adjacent column text, section headings, or page numbers
- After cropping, verify the exported image contains only the target figure

### Composite Figures

If a figure is composed of multiple PDF objects (overlays, annotations, arrows), render the page region rather than exporting individual objects. The output must match what the PDF viewer displays.

## Tables

| Priority | Method | When to Use |
|----------|--------|-------------|
| 1 | Markdown table | Simple structure, fits in columns |
| 2 | HTML table | Complex rowspan/colspan, wide tables |
| 3 | Annotated screenshot | Cannot reliably reconstruct |

For screenshot fallback:
- Include caption and full table body in the crop
- For multi-page tables, stitch pages or use sequential images with consecutive Markdown references
- Verify header row, last row, and caption are all captured before delivery

## Equations

- Inline: `$...$` / Block: `$$...$$`
- Preserve original variable names, subscripts, superscripts, Greek letters, and equation numbers exactly
- Translate surrounding explanation text, but leave the equation itself untouched
- If extraction fails: attempt manual LaTeX transcription first; if unreliable, keep equation as image with degradation note
