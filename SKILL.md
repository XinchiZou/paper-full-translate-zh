---
name: paper-full-translate-zh
description: "Translate academic papers into structured Chinese Markdown with full fidelity — preserving figures, captions, tables, equations, and appendices. Creates a paper-title directory containing the original file, zh-CN full translation, research notes with an onion-peeling literature guide (剥洋葱式文献导读), and exported image assets. Use when: user requests full-text paper translation to Chinese, paragraph-by-paragraph academic paper translation, preserve figures/tables/formulas in Markdown output, organized research asset directory, or 全文翻译论文并保留图片图表公式输出 Markdown。"
license: MIT
metadata:
  author: workspace
  version: "0.5.3"
---

# Paper Full Translate Zh

Translate user-provided papers into readable, traceable Chinese Markdown with supplementary research notes.
The full translation file (full.md) faithfully reconstructs the body text; the onion-peeling literature guide (剥洋葱式文献导读) belongs at the top of notes.md, not in full.md.

## Output Structure

```text
<paper_title_dir>/
  <original_paper_filename>.pdf
  <paper_stem>.zh-CN.full.md
  <paper_stem>.zh-CN.notes.md
  assets/                          # always named assets/ — keep paths short
```

**Naming rules:**
- Directory: paper title (filesystem-safe); falls back to original filename stem if title is unavailable
- `assets/` is a fixed short name — never embed the paper title in the assets directory path
- Local paper files are moved (not copied) into the directory; remote papers are saved directly there
- Reuse existing directories; do not create parallel duplicates

## When to Apply

**Use** when the user asks to translate a full paper to Chinese, preserve figures/tables/equations, output as Markdown, or organize results into a named directory with reading notes.

**Do not use** for summary-only translation, literature reviews without full-text fidelity, or when no paper source is provided.

## Defaults & Confirmation Points

Use these defaults if the user does not specify; note them in the output. On first use with a new user, confirm items marked ⚠ to avoid rework:

| Input | Default | Confirm? |
|-------|---------|----------|
| Directory naming | Paper title → filename stem fallback | ⚠ user may want a custom name |
| Output language | Chinese only (no bilingual) | ⚠ user may want bilingual |
| Notes format | Separate .notes.md file | ⚠ user may want merged single file |
| Onion guide | Top of notes.md | |
| Image export | Export to `assets/` with relative paths | |
| References | Keep original citation strings | ⚠ user may want titles translated |
| OCR for scanned PDFs | Allowed, marked with risk warning | ⚠ confirm tolerance |

## Workflow

### 1. Validate the Source

Identify source type and select extraction strategy:

| Priority | Source | Notes |
|----------|--------|-------|
| 1 | Structured HTML / LaTeX | Best fidelity |
| 2 | Text-extractable PDF | Cross-check with visual layout for multi-column/floats |
| 3 | Scanned PDF (OCR) | Warn user about accuracy |

If both structured source and PDF exist, cross-check title/author/sections to avoid version mismatch.

### 2. Create the Paper Directory

Before generating any output:
1. Determine the paper title
2. Create a filesystem-safe directory from it
3. Move or save the source file into the directory
4. All subsequent outputs go inside this directory

### 3. Build a Structural Map

Before translating, inventory the full paper structure:
- Title, authors, abstract, keywords
- All section headings and their hierarchy
- Equation numbers and positions
- Figure/table numbers, captions, and reference locations
- Footnotes, appendices, acknowledgements, references

Every translated paragraph must trace to a specific source location. No summarize-then-expand. No silent omissions. For complex papers with many figures/tables/equations, a temporary extraction script is acceptable as an intermediate tool (delete it after delivery).

### 4. Extract Figures, Tables, and Equations

See [EXTRACTION.md](EXTRACTION.md) for detailed extraction rules, multi-column handling, and fallback strategies.

**Key principles:**
- **Figures**: export to `assets/figure-NN.png` using page-area rendering (not raw image objects); verify crops contain only the target figure
- **Tables**: Markdown table → HTML table → annotated screenshot, in order of preference
- **Equations**: preserve as LaTeX (`$...$` / `$$...$$`); keep original variable names and numbering
- **Degradation**: if any element cannot be faithfully extracted, keep a screenshot or fragment and mark it explicitly — never silently drop content

**Quick figure extraction example (PyMuPDF):**

```python
import fitz
page = fitz.open("paper.pdf")[page_num]
clip = fitz.Rect(x0, y0, x1, y1)  # figure bounding box
pix = page.get_pixmap(matrix=fitz.Matrix(2, 2), clip=clip, alpha=False)
pix.save("assets/figure-01.png")
```

### 5. Translate Without Omissions

- Translate paragraph by paragraph — no skipping, no merging multiple paragraphs into summary-style Chinese
- Process all section headings, figure captions, table captions, footnotes, appendices
- Do NOT translate: equations, code, pseudocode, algorithm names, dataset names, model names (add brief Chinese gloss after if needed)
- Technical terms on first occurrence: "中文（English）"; keep consistent afterwards
- Uncertain phrases: preserve the original and add a cautious Chinese interpretation nearby
- If a passage cannot be reliably extracted, insert: "此处原文提取不稳定，建议人工复核"

### 6. Reconstruct the Markdown

```markdown
# 中文标题

## 论文信息
- 原文标题：...
- 作者：...
- 来源：...
- 原文件：<paper_title_dir>/<original_paper_filename>

## 摘要
...

## 1 引言
...

![Figure 1: ...](assets/figure-01.png)

$$...$$

## 参考文献
...
```

Preserve original section hierarchy and numbering. Place figures and tables near their first in-text reference.

### 7. Write the Onion-Peeling Guide and Notes

See [NOTES_TEMPLATE.md](NOTES_TEMPLATE.md) for the complete specification and template.

The onion-peeling guide (剥洋葱式文献导读) goes at the top of notes.md with four fixed steps:
1. **Context**: one sentence on the real problem being solved
2. **Grounding**: a concrete everyday metaphor for the core mechanism
3. **Core Focus**: deconstruct 1–2 key equations, mapping symbols to the metaphor
4. **Exhaustive Mapping**: fill in remaining formulas and definitions into the main story

The rest of notes.md contains research notes: metadata, core problem, method overview, contributions, experiments, strengths/limitations, relevance, and follow-up questions.

### 8. Completion Checks

- [ ] Section count matches original structure
- [ ] No missing abstract, appendix, captions, footnotes, acknowledgements, references
- [ ] Original paper file moved into the directory
- [ ] full.md, notes.md, and assets/ all in the same directory
- [ ] All image links resolve with relative paths
- [ ] Tables readable, equations preserve original meaning
- [ ] Onion-peeling guide at the top of notes.md with all 4 steps complete
- [ ] All unreliable extractions explicitly marked

## Decision Rules

| Scenario | Action |
|----------|--------|
| arXiv source | Prefer structured HTML/LaTeX for text; use PDF for image cross-checking |
| Normal PDF with text | Extract text first, cross-check visual layout for multi-column and floats |
| Scanned PDF | Warn about OCR accuracy; prioritize completeness over formatting |
| Imperfect figure/equation | Degrade to screenshot with annotation; never silently drop |

## Example Prompts

- 把这篇 PDF 收进一个以论文名命名的目录里，原文件剪切进去，再生成全文中文 Markdown、notes 和 assets。
- 处理这个 arXiv 论文链接，创建论文名称目录，并把下载的原论文、中文全文 md、notes 文件和 assets 一起放进去。
- 对这篇论文做逐段翻译，不要省略 appendix，公式用 LaTeX，图表尽量原位保留。
- Translate this paper to Chinese Markdown, keep all figures and equations, organize into a named directory.

