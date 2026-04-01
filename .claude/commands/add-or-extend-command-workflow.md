---
name: add-or-extend-command-workflow
description: Workflow command scaffold for add-or-extend-command-workflow in everything-claude-code.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /add-or-extend-command-workflow

Use this workflow when working on **add-or-extend-command-workflow** in `everything-claude-code`.

## Goal

Adds a new command or extends an existing command, including documentation and review feedback fixes.

## Common Files

- `commands/*.md`
- `README.md`
- `docs/*`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Create or update commands/<command-name>.md
- Document usage, output, and YAML frontmatter
- Incorporate review feedback (fix placeholders, clarify sections, update templates)
- Update references in README.md or related docs

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.