---
name: academic-presentation
description: "Create academic presentations from papers, posters, or review materials using deterministic conference and literature-review presets. Use when the user asks to make slides, prepare a talk, build a Beamer deck, or turn review content into a presentation."
---

# Academic Presentation Skill

## Purpose

Create academic presentations from papers, posters, or review materials using deterministic conference and literature-review presets. Use when the user asks to make slides, prepare a talk, build a Beamer deck, or turn review content into a presentation.

Keep this `SKILL.md` as a concise routing and execution entrypoint. Do not load
long examples, command catalogs, detailed checklists, or edge-case policy until
the current task needs them.

## Workflow

1. Confirm the user request matches this skill's frontmatter description.
2. Bind the concrete target: source file, artifact, repo, device, document,
   dataset, or user-facing deliverable.
3. Use the smallest relevant workflow from this entrypoint first.
4. Before choosing a presentation preset, building Beamer/PPTX content,
   composing figures, embedding video, cleaning deck directories, or declaring
   the rendered deck ready, read `references/entrypoint-details.md`.
5. Preserve local owner boundaries: route to a narrower skill or repo-specific
   workflow when the detailed reference indicates a more specific owner.

## Detailed Reference

Read `references/entrypoint-details.md` for:

- Deterministic routing
- Workflow
- Conference preset
- Literature review preset
- Figure composition from existing PDFs
- Column alignment in Beamer
- Beamer implementation reference
- Visual QA (Required)
- Consistency checklist (run before declaring ready)
- Output conventions
- Directory cleanup
- Video in presentations
- Validation And Checkpoints

## Validation

- Use the skill-specific validation or acceptance checks from the detailed
  reference before declaring completion.
- When editing this skill, run `quick_validate.py` on the skill directory and
  verify all referenced files still exist.
