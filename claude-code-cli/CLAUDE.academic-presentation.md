# Academic Presentation

Use this workflow when the user asks to make slides, prepare a talk, build a Beamer deck, or turn papers, posters, or review materials into a presentation.

This workflow owns:
- conference, seminar, defense, and finalist decks
- literature-review and taxonomy decks

Keep upstream review synthesis separate:
- use an upstream review workflow to define scope, build the corpus, classify papers, and produce matrices or outline content
- use this workflow to turn that prepared content into the final deck

Route ordinary `.pptx` work through the host environment:
- use the host's primary editable `.pptx` workflow for ordinary deck authoring and deck editing
- use a low-level `.pptx` workflow only for XML inspection or template-preserving edits

## Deterministic routing

Resolve the deck path in this order:

1. If the user explicitly names a format or preset, follow it.
2. If the user explicitly asks for editable `.pptx` output, route to the host's primary editable `.pptx` workflow.
3. If the task is primarily low-level `.pptx` template work, route to a low-level `.pptx` workflow.
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
- reference-heavy review or group-meeting deck

If both signal sets appear, oral-talk constraints win and the default is `conference preset`.

## Workflow

### 1. Gather context

Inspect the real source material first:
1. Read the paper, poster, review outline, or prepared matrix. Prefer `.tex` when available.
2. Record delivery constraints: audience, duration, slide count, output format, template, deadline.
3. Inventory visual assets in the project directory: figures, tables, screenshots, logos, and videos.
4. If a repository is referenced, inspect the README and the specific assets actually needed for the deck.

### 2. Lock the presentation mode

Write down these decisions before drafting slides:
- preset: `conference` or `literature review`
- format: `beamer` or `.pptx`
- source-of-truth deliverable
- output directory
- whether asset localization is required

If the user does not pick a format, default to Beamer when the source is paper-first, LaTeX-first, or PDF-first.

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

- Use `Beamer` for paper-first or PDF-first decks, math-heavy content, review decks, or when PDF is the main deliverable.
- Use the host's primary editable `.pptx` workflow when editable `.pptx` output is explicitly required.
- Use a low-level `.pptx` workflow only when an existing template must be preserved through XML-level or template-preserving edits.

### 5. Draft the deck

Write the authoring source in a task-local output directory.

If the deck is Beamer-based:
- localize referenced figures into the output directory when portability matters
- keep `.tex` and generated PDF together
- compile twice by default when cross-references or total frame counts are involved
- default to a restrained academic baseline such as 16:9 `metropolis`, white background, one accent color, and consistent footer behavior

If the deck is `.pptx`-based:
- keep the authoring source and rendered `.pptx` together
- use the host's primary editable `.pptx` workflow rather than forcing a PDF-first Beamer path

### 6. Run visual QA before delivery

Every presentation must pass visual inspection before delivery.

1. Compile and fix actual errors first.
2. For Beamer, render the PDF pages as images and inspect those images, not just the `.tex`.
3. Use rendered-deck visual QA as the default final gate before reporting the deck as ready.
4. Look for:
   - leaked LaTeX commands rendered as text
   - duplicate page numbers
   - figures not rendering or rendering at the wrong scale
   - tables with broken alignment
   - text or figures clipped at slide edges
   - repeated main visuals across adjacent slides when the narrative role is redundant
5. If the user-visible deliverable is report-class, run a source-text quality scan on the edited authoring source before reporting completion.
6. Only after the PDF or deck passes the rendered-deck visual QA gate should you present it as ready.

## Output conventions

- Create a dedicated output directory for the deck.
- Localize referenced assets into that directory when portability matters.
- Keep the authoring source beside the built deliverable.
- Follow the user or venue naming rule for the final file.
- Do not silently build extra artifacts the user did not request.
