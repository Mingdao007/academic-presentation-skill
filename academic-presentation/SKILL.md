---
name: academic-presentation
description: "Create academic presentations from papers, posters, or review materials using deterministic conference and literature-review presets. Use when the user asks to make slides, prepare a talk, build a Beamer deck, or turn review content into a presentation."
---

# Academic Presentation Skill

Create final presentation artifacts from papers, posters, or prepared review content.

This skill is the presentation-authoring owner for:
- conference / seminar / defense / finalist decks
- literature-review and taxonomy decks

Keep upstream review synthesis separate:
- use `literature-review-workflow` to define scope, build the corpus, classify papers, and produce matrices or outline content
- use this skill to turn that prepared content into the final deck

Route ordinary `.pptx` work elsewhere:
- use `slides` for primary `.pptx` authoring and deck editing
- use `pptx` for low-level `.pptx` inspection, XML unpacking, or template-preserving edits

## Deterministic routing

Resolve the deck path in this order:

1. If the user explicitly names a format or preset, follow it.
2. If the user explicitly asks for editable `.pptx` output, route to `slides`.
3. If the task is primarily low-level `.pptx` template work, route to `pptx`.
4. Otherwise, choose between the two Beamer presets below.

### Preset selection

Use `conference preset` when the request contains oral-talk signals such as:
- `conference`
- `finalist`
- `seminar`
- `defense`
- duration or slide-count constraints
- `Q&A`
- speaker notes or speaking flow

Use `literature review preset` when the request contains review-deck signals such as:
- `literature review`
- `taxonomy`
- `classification`
- `comparison`
- `survey`
- reference-heavy advisor or group-meeting deck

If both signal sets appear, oral-talk constraints win and the default is `conference preset`.

## Workflow

### 1. Gather context

Inspect the real source material first:
1. Read the paper, poster, review outline, or prepared matrix. Prefer `.tex` when available.
2. Record delivery constraints: audience, duration, slide count, output format, template, deadline.
3. Inventory visual assets in the project directory: figures, tables, screenshots, logos, videos.
4. If a repository is referenced, inspect the README and the specific assets actually needed for the deck.

### 2. Lock the presentation mode

Write down these decisions before drafting slides:
- preset: `conference` or `literature review`
- format: `beamer` or `.pptx`
- source-of-truth deliverable
- output directory
- whether asset localization is required

If the user did not pick a format, default to Beamer when the source is paper-first, LaTeX-first, or PDF-first.

### 3. Build the structure

For `conference preset`:
- target roughly one minute per slide for a short talk
- use a narrative arc such as motivation -> challenge -> approach -> validation -> results -> insights -> conclusion
- keep background theory to one slide unless the method truly needs more
- prefer visual explanations over prose-heavy slides

For `literature review preset`:
- lead with the classification or taxonomy, not with search-process narration
- organize the deck around method structure, class boundaries, and comparison logic
- prefer flowcharts, mind maps, comparison tables, and short evidence cards
- keep paper-title formatting and venue tags consistent across the deck
- split crowded structure slides before shrinking the font aggressively

### 4. Choose the authoring tool

| Tool | Use when |
|------|----------|
| **Beamer** | Paper-first or PDF-first deck, math-heavy content, review deck, or when PDF is the main deliverable |
| **slides** | Editable `.pptx` is explicitly required |
| **pptx** | Existing template must be preserved through low-level `.pptx` operations |

### 5. Draft the deck

Write the authoring source in a task-local output directory.

If the deck is Beamer-based:
- localize referenced figures into the output directory when portability matters
- keep `.tex` and generated PDF together
- compile twice by default when cross-references or total frame counts are involved

If the deck is `.pptx`-based:
- keep the authoring source and rendered `.pptx` together
- delegate the implementation details to `slides`

### 6. Generate custom figures when tables should become visuals

When quantitative paper tables would be clearer as plots, generate a small reproducible script and export both PDF and PNG.

```python
"""Template: reproducible plot from paper values."""
import matplotlib
matplotlib.use("Agg")
import matplotlib.pyplot as plt
import numpy as np

plt.rcParams.update(
    {
        "font.size": 9,
        "figure.dpi": 200,
        "savefig.dpi": 300,
        "savefig.bbox": "tight",
        "font.family": "sans-serif",
    }
)

data = {
    "Model A": [0.041, 0.109],
    "Model B": [0.006, 0.034],
}

# plotting logic here

fig.savefig("figure.pdf")
fig.savefig("figure.png")
```

Guidelines:
- use `Agg` for headless rendering
- save both PDF and PNG
- use `np.nan` for missing values so the plot reflects gaps honestly
- mark divergent cases explicitly instead of hiding them
- highlight the best method with a visually distinct style

## Conference preset

Use this preset for short oral presentations such as conference talks, finalist decks, seminars, or defenses.

### Structure baseline

| Slide | Content | Typical visual |
|-------|---------|----------------|
| 1 | Title, authors, affiliations, conference | --- |
| 2 | Motivation / why this matters | Application photo/diagram |
| 3 | The problem / challenge | System diagram or data showing the gap |
| 4 | Background theory (1 slide max) | Key equations only |
| 5 | Approach / method | Pipeline diagram or equations |
| 6 | Model/algorithm details | Table or block diagram |
| 7 | Validation on simple system | Validation plots |
| 8 | Experimental setup | Simulation/hardware photos |
| 9 | Task details (optional) | Trajectory/task visualization |
| 10-11 | Results (2 slides: baseline → proposed) | Tables + plots |
| 12 | Result visualization | Time-series / rollout plots |
| 13 | Key insights / takeaways | Numbered list |
| 14 | Conclusion + future work + Q&A | Two-column layout |

### Visual baseline

This preset inherits the mature ODE-licious-style baseline:
- 16:9 Beamer with `metropolis`
- white academic background
- one restrained accent color
- logo-led title page
- left-text / right-figure content pages
- lightweight citation footer
- visible but restrained page numbering and progress bar
- use `shrink` only as an overflow fallback, not as the first layout tool

## Literature review preset

Use this preset for taxonomy decks, survey presentations, advisor decks, and reference-heavy method comparisons.

### Structure baseline

- open with the field split, taxonomy, or comparison frame
- keep the deck centered on class boundaries, representative papers, and synthesis
- use mind maps, flowcharts, comparison tables, and short method cards
- keep card titles and paper tags readable
- use reference slides when in-body citations become too dense

### Visual baseline

This preset inherits the stable literature-review style:
- title slide can carry a stronger visual identity than the content slides
- content slides prefer structured cards, blocks, and TikZ diagrams
- classification pages may use card hierarchies and arrows
- comparison slides should read cleanly as review artifacts, not as oral-talk scripts
- tables, tags, and block headers must stay consistent across the deck

## Figure composition from existing PDFs

When raw data is unavailable but a combined figure is needed (e.g., stacking multiple plots into one):

```python
"""Compose multiple PDF figures into one using pymupdf + PIL."""
import fitz
from PIL import Image
import numpy as np

DPI = 400
SCALE = DPI / 72

def render_pdf(path):
    doc = fitz.open(path)
    page = doc[0]
    pix = page.get_pixmap(matrix=fitz.Matrix(SCALE, SCALE))
    img = Image.frombytes("RGB", [pix.width, pix.height], pix.samples)
    doc.close()
    return img

# Crop titles/legends by percentage
arr = np.array(img)
cropped = Image.fromarray(arr[int(arr.shape[0] * 0.07):])  # remove top 7%

# Scale to same width, stack with gap
combined = Image.new("RGB", (w, h1 + gap + h2), "white")
combined.paste(img1, (0, 0))
combined.paste(img2, (0, h1 + gap))
combined.save("combined.pdf", "PDF", resolution=DPI)
```

Guidelines:
- 400 DPI is sufficient for projected presentations
- crop baked-in titles rather than overlaying white rectangles
- when models differ between subplots, note the legend discrepancy
- keep source figures alongside the combined output (scripts may need to regenerate)

## Column alignment in Beamer

| Alignment | `\begin{columns}[?]` | Use when |
|-----------|----------------------|----------|
| Top | `[T]` | Text-heavy slides, tables beside text, figure+text where both start at top |
| Center | `[c]` | Two figures side by side, symmetric content |
| Mixed | `[T]` + manual centering | Figure should center but text should top-align — but `\vfill` does NOT work inside columns; use `[T]` and let the tall figure fill naturally |

Key lesson: `\vfill` and `\vspace*{\fill}` do not expand inside Beamer columns because column height is content-determined, not frame-determined. For figure-left + text-right slides, `[T]` is usually the right choice when the figure is tall enough to fill the column naturally.

## Beamer implementation reference

Load `references/beamer-presets.md` when you need:
- preset selection rules
- common Beamer skeletons
- title page, two-column, 2x2 grid, comparison table, reference footer, and TikZ classification patterns
- compile and portability checklist
- known failure modes and fixes

## Visual QA (Required)

Every presentation must pass visual inspection before delivery.

1. Compile and fix actual errors first.
2. For Beamer, render the PDF pages as images and inspect those images, not just the `.tex`.
3. Look for:
   - leaked LaTeX commands rendered as text
   - duplicate page numbers
   - figures not rendering or rendering at the wrong scale
   - tables with broken alignment
   - text or figures clipped at slide edges
   - repeated main visuals across adjacent slides when the narrative role is redundant
4. If the user-visible deliverable is report-class, run `python3 $CODEX_HOME/skills/ai-detect/scripts/scan_ai_smell.py <source>` on the edited authoring source before reporting completion.
5. Only after the PDF or deck passes visual QA should you present it as ready.

## Consistency checklist (run before declaring ready)

Run this checklist across the full `.tex` before final delivery:

1. **Model/method naming** — same model must use the same string everywhere (tables, text, figure references)
2. **Notation** — mathematical sets vs model-name brackets (e.g., $\{1,5,10\}$ for sets, $[1,5,10]$ for model names)
3. **Terminology** — "X Y" vs "XY", "1-step" vs "one-step"; pick one and apply globally
4. **Data values** — cross-check every number in tables against the paper source
5. **Improvement claims** — verify ratios (e.g., "2.5×") by computing from the actual table values
6. **Comment numbering** — `% Slide N` comments must match actual frame order
7. **Unused definitions** — grep for `\newcommand`, `\definecolor`, `\usepackage` that are never referenced
8. **Column width sums** — left + right column widths should not exceed 1.0 (leave ~0.04 gap)
9. **Figure file references** — every `\includegraphics` file must exist in the output directory

## Output conventions

- Create a dedicated output directory for the deck.
- Localize referenced assets into that directory when portability matters.
- Keep the authoring source beside the built deliverable.
- Follow the user or venue naming rule for the final file.
- Do not silently build extra artifacts the user did not request.

## Directory cleanup

After the deck is stable, audit the output directory:
- keep: `.tex`, output PDFs, referenced figures, logos, plotting scripts, source figures used by scripts
- remove: unused figures (e.g., cropped versions replaced by originals), PNG duplicates not referenced, unused logos, LaTeX build artifacts (`.aux .log .nav .out .snm .toc .fls .fdb_latexmk`)
- move to `_unused/` first if unsure, then delete once confirmed

## Video in presentations

| Approach | Pros | Cons |
|----------|------|------|
| Beamer `multimedia` package | Single PDF file | Only works in Adobe Acrobat |
| Switch to pptx (python-pptx) | Native video embedding | Need to rebuild slides |
| Alt+Tab to video player | Most reliable | Requires presenter coordination |
| Convert to animated GIF screenshot | Works in PDF | Loses video quality |

Recommendation:
- for critical embedded video, prefer `.pptx`
- otherwise keep videos as separate playback assets instead of forcing them into a PDF
