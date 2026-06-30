# Jasson's Agent Skills

[![skills.sh](https://skills.sh/b/jassonbla/skills)](https://skills.sh/jassonbla/skills)

Personal Agent Skills by [jassonbla](https://github.com/jassonbla).

This repository is a home for reusable agent workflows, instructions, templates, and reference materials. Each skill is self-contained under `skills/<skill-name>/` and includes a `SKILL.md` file with the instructions and metadata an agent needs to load it dynamically.

## Install

Install all discoverable skills from this repository:

```bash
npx skills add jassonbla/skills
```

List available skills:

```bash
npx skills add jassonbla/skills --list
```

Install a specific skill:

```bash
npx skills add jassonbla/skills --skill daily-tech-briefing
npx skills add jassonbla/skills --skill git-insight
npx skills add jassonbla/skills --skill coding-workflow
```

## Claude Code plugin marketplace

This repository can also be registered as a Claude Code plugin marketplace:

```text
/plugin marketplace add jassonbla/skills
```

Then install the bundled personal skills plugin:

```text
/plugin install personal-skills@jasson-agent-skills
```

## Skills

### `daily-tech-briefing`

Create a personalized daily technology briefing from RSS or web source lists.

Contents:

```text
skills/daily-tech-briefing/SKILL.md
skills/daily-tech-briefing/references/sources.default.json
skills/daily-tech-briefing/references/source.schema.json
skills/daily-tech-briefing/references/briefing-template.md
skills/daily-tech-briefing/examples/sources.personal.json
skills/daily-tech-briefing/examples/briefing.example.md
skills/daily-tech-briefing/examples/feedback.example.md
```

Install only this skill:

```bash
npx skills add jassonbla/skills --skill daily-tech-briefing
```

### `git-insight`

Analyze git commit history and summarize recent activity from a mission or project perspective.

Contents:

```text
skills/git-insight/SKILL.md
skills/git-insight/references/report-template.md
skills/git-insight/examples/example-report.md
```

Install only this skill:

```bash
npx skills add jassonbla/skills --skill git-insight
```

### `coding-workflow`

Run coding tasks with a disciplined, PR-oriented agent workflow: clarify scope, inspect repository context, isolate work, delegate when useful, validate, and report evidence.

Contents:

```text
skills/coding-workflow/SKILL.md
skills/coding-workflow/references/checklist.md
skills/coding-workflow/examples/worker-brief.md
```

Install only this skill:

```bash
npx skills add jassonbla/skills --skill coding-workflow
```

## Repository layout

```text
.claude-plugin/marketplace.json  # Claude Code plugin marketplace manifest
skills/                         # Skill packages
template/SKILL.md.template       # Minimal starting template for new skills
docs/                           # Repository-level notes and conventions
```

## Skill format

A skill is a folder with a required `SKILL.md` file:

```text
skills/my-skill/
├── SKILL.md
├── references/   # optional durable reference files
├── examples/     # optional examples and fixtures
├── scripts/      # optional executable helpers; document safety clearly
└── assets/       # optional media or static assets
```

`SKILL.md` should start with YAML frontmatter:

```yaml
---
name: my-skill
description: What this skill does and when an agent should use it.
---
```

## Safety and privacy

- Do not commit credentials, tokens, private chat IDs, paid-newsletter content, or private customer data.
- Prefer examples and templates over personal state.
- If a skill includes scripts, document what they do, required dependencies, and safe usage.
- Keep personal configuration in the user's agent workspace, not in this public repository.

## Publishing model

There is no separate skills.sh submission flow. A skill is published by putting it in a public git repository and sharing it. When users install it with `npx skills add`, it can appear on skills.sh through anonymous install telemetry.

## License

MIT
