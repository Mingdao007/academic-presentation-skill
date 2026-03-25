# Academic Presentation Skill

Portable presentation-authoring skill for turning papers, posters, and review materials into final academic decks. Works with Codex App and Claude CLI.

## What Ships

- installable skill: [`academic-presentation`](./academic-presentation)
- Codex App metadata: [`academic-presentation/agents/openai.yaml`](./academic-presentation/agents/openai.yaml)
- bundled public references: [`academic-presentation/references/`](./academic-presentation/references)
- Claude CLI excerpt: [`claude-code-cli/CLAUDE.academic-presentation.md`](./claude-code-cli/CLAUDE.academic-presentation.md)

## Install / Use

### Codex App

- Install the skill from this repo path: `academic-presentation`
- GitHub install target:
  - repo: `<owner>/academic-presentation-skill`
  - path: `academic-presentation`
- Restart `Codex App` after installation so the new skill is discovered.

### Claude CLI

- Open [`claude-code-cli/CLAUDE.academic-presentation.md`](./claude-code-cli/CLAUDE.academic-presentation.md)
- Copy the full excerpt into your project `CLAUDE.md`
- Keep it as one dedicated section so future updates stay easy to diff and replace
- Restart the Claude CLI session if your setup only reads `CLAUDE.md` at session start

## Coverage

- conference, seminar, defense, and review-deck routing
- deterministic preset selection between oral-talk and literature-review decks
- paper-first presentation workflow with reusable public references
- rendered-deck visual QA and report-class source-text scan guidance

## Trigger Examples

- `Make a literature-review deck from these papers.`
- `Turn this poster into a short talk deck.`
- `Prepare a seminar presentation from this paper.`

## Non-Trigger Examples

- `Edit one existing .pptx template at the XML level.`
- `Do a full literature review from scratch.`
- `Only explain one slide or one paragraph.`

## Privacy Boundary

This public repository keeps the workflow generic and reusable.

- Examples stay generic and omit private project, course, or advisor context.
- This package publishes no local absolute paths, private workspace references, or host-specific private skill links.

## Repository Layout

- `academic-presentation/`: installable `Codex App` skill
- `academic-presentation/agents/openai.yaml`: `Codex App` interface metadata
- `academic-presentation/references/`: bundled public references
- `claude-code-cli/CLAUDE.academic-presentation.md`: copyable `Claude CLI` excerpt
- `CHANGELOG.md`: release history
- `LICENSE`: `MIT`

Chinese:

- [README.zh-CN.md](./README.zh-CN.md)
