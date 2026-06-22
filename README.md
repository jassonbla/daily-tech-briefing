# Daily Tech Briefing

[![skills.sh](https://skills.sh/b/jassonbla/daily-tech-briefing)](https://skills.sh/jassonbla/daily-tech-briefing)

A portable Agent Skill for creating a personalized daily technology briefing from RSS and web sources.

It starts with a curated default source set for AI, developer tools, cloud infrastructure, product strategy, and editorial analysis, then gives users a simple path to add their own RSS feeds and tune future recommendations.

## Install

```bash
npx skills add jassonbla/daily-tech-briefing
```

Install only this skill if your agent asks for a specific skill:

```bash
npx skills add jassonbla/daily-tech-briefing --skill daily-tech-briefing
```

List discoverable skills in this package:

```bash
npx skills add jassonbla/daily-tech-briefing --list
```

## What it does

- Builds a daily tech briefing from RSS/web source lists.
- Includes a default curated source registry.
- Helps users add personal RSS sources without changing the skill itself.
- Ranks items by relevance, novelty, credibility, and actionability.
- Keeps dedupe, read-later, and feedback loops explicit.
- Lays groundwork for future personalized source suggestions.

## Package contents

```text
skills/daily-tech-briefing/SKILL.md
skills/daily-tech-briefing/references/sources.default.json
skills/daily-tech-briefing/references/source.schema.json
skills/daily-tech-briefing/references/briefing-template.md
skills/daily-tech-briefing/examples/sources.personal.json
skills/daily-tech-briefing/examples/briefing.example.md
skills/daily-tech-briefing/examples/feedback.example.md
```

## Customizing sources

Copy `examples/sources.personal.json` into your own agent workspace or project and edit it. Keep the default registry as a reference, not as your personal state file.

Recommended fields:

- `name` — human-readable source name
- `url` — RSS/Atom feed URL or source URL
- `type` — `rss`, `atom`, `newsletter`, `web`, or `manual`
- `category` — one of the categories in `source.schema.json`
- `priority` — 0.0 to 1.0 baseline ranking weight
- `signals` — topics this source is good for
- `rationale` — why it belongs in your briefing
- `status` — `default`, `personal`, `candidate`, `muted`, or `archived`

## Safety and privacy

This package does not include executable scripts in v1. It is a skill, templates, and source registries only.

When using this skill with an agent:

- Review external links before relying on them.
- Do not paste private paid-newsletter content into public repositories.
- Ask before adding, muting, or deleting persistent sources.
- Use your agent's scheduler/reminder system for automation; this skill does not install cron jobs.

## Publishing model

There is no separate skills.sh submission flow. A skill is published by putting it in a public git repo and sharing it. When users install it with `npx skills add`, it can appear on skills.sh through anonymous install telemetry.

## License

MIT
