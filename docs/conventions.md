# Skill Repository Conventions

This repository stores reusable Agent Skills under `skills/<skill-name>/`.

## Required

- `SKILL.md` with `name` and `description` YAML frontmatter.
- Clear trigger conditions in the description.
- Instructions that are specific enough to be repeatable.

## Optional folders

- `references/` for durable reference files and schemas.
- `examples/` for sample inputs/outputs and fixtures.
- `scripts/` for helper scripts. Scripts must include safety notes in the skill.
- `assets/` for static media or templates.

## Privacy

Do not commit credentials, tokens, private IDs, private customer data, or personal runtime state.
