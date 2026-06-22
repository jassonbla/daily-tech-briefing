---
name: daily-tech-briefing
description: Create a personalized daily technology briefing from RSS or web source lists. Use when the user asks for a daily tech briefing, technology news digest, AI/cloud/devtools update, RSS curation, source tuning, or personalized briefing workflow.
license: MIT
metadata:
  version: "1.0.0"
  source_registry: references/sources.default.json
  source_schema: references/source.schema.json
  template: references/briefing-template.md
---

# Daily Tech Briefing

Create a concise, high-signal daily technology briefing from RSS and web source lists. The skill is source-registry driven: start from the default sources, merge any user-provided sources, then rank and summarize recent items for the user's interests.

## What this skill does

- Collects recent technology updates from RSS/Atom/web sources available to the agent.
- Prioritizes AI, developer tools, cloud infrastructure, product strategy, creator economy, security, and market/editorial analysis.
- Produces a briefing with clear sections, source links, and short implications.
- Helps the user maintain a personal source registry.
- Uses feedback from prior briefings to propose source additions, removals, and priority changes.

## When to use

Use this skill when the user asks for:

- "daily tech briefing"
- "tech briefing"
- "today's AI news"
- "RSS briefing"
- "technology digest"
- "source curation"
- "add this RSS to my briefing"
- "tune my briefing sources"

Do not use it for general web research that is not meant to become a recurring briefing workflow.

## Inputs to look for

Ask at most one clarifying question if the request is ambiguous. Otherwise proceed with reasonable defaults.

Useful inputs:

- Date or time window, default: last 24-48 hours.
- Region or language preference.
- User source registry path, if any.
- Topics to emphasize or avoid.
- Desired length: short, normal, deep.
- Delivery target or scheduler preference, if the agent supports scheduling.

## Source registry

The default registry is in `references/sources.default.json`. Treat it as a starting point, not immutable truth.

Users can keep their own registry in a project or workspace file such as:

- `daily-tech-briefing.sources.json`
- `references/daily-tech-briefing/sources.personal.json`
- an agent memory/wiki page

When both default and personal sources exist:

1. Load the default sources.
2. Load user sources.
3. Merge by canonicalized URL first, then by normalized source name.
4. Let user `status` override default status.
5. Let user `priority` override default priority only for that user.

Never silently edit a user's persistent source registry. Propose changes and ask for approval before writing.

## Source categories

Use the schema in `references/source.schema.json`. Preferred categories:

- `ai-labs`
- `developer-tools`
- `cloud-infra`
- `security-risk`
- `product-strategy`
- `creator-economy`
- `market-analysis`
- `editorial-analysis`
- `research`
- `company-news`

## Briefing procedure

### 1. Prepare sources

- Load default sources from `references/sources.default.json` if available.
- Load user-provided sources if available.
- Exclude sources with `status: muted` or `status: archived` unless the user explicitly asks to inspect them.
- For each active source, note its `priority`, `signals`, and `rationale`.

### 2. Collect recent items

Use available RSS, web fetch, browser, or search tools. Prefer RSS/Atom when possible because it is repeatable.

For each item, capture:

- title
- url
- source name
- published time if available
- author if available
- short excerpt or summary
- tags/signals inferred from the content

If a source fails, continue with other sources and include a short failure note only if it affects coverage.

### 3. Deduplicate

Deduplicate before ranking:

- canonical URL match
- same normalized title
- same announcement covered by multiple outlets
- syndication/cross-posts

When duplicates exist, prefer the primary/original source. Keep secondary analysis only if it adds meaningful interpretation.

### 4. Rank

Rank items with a practical score. Favor:

- direct impact on builders, product teams, AI workflows, infra, security, or market strategy
- novelty versus previous briefings
- credible primary sources
- actionable details over generic commentary
- high-signal analysis from trusted writers
- user-stated interests and feedback

Downrank:

- low-detail launch posts
- SEO-farm summaries
- duplicated wire coverage
- speculation without evidence
- items outside the user's stated scope

Suggested scoring factors:

```text
score = source_priority
      + relevance
      + novelty
      + actionability
      + credibility
      + user_feedback_fit
      - duplication_penalty
      - hype_penalty
```

### 5. Write the briefing

Use `references/briefing-template.md` as the default format.

Keep the output concise. Each item should answer:

- What happened?
- Why does it matter?
- What should the reader consider doing or watching next?

Always include source links.

### 6. Add source tuning notes

At the end, include lightweight source tuning only when useful:

- sources that were noisy
- sources that repeatedly produced high-signal items
- candidate sources to add
- categories that need better coverage

Do not auto-add candidate sources. Ask for approval before persisting.

## Personalization loop

When the user gives feedback, record it in the user's chosen memory or source registry if they approve.

Useful feedback dimensions:

- `more_like`: source, topic, item, or writing style to increase
- `less_like`: source, topic, item, or writing style to decrease
- `mute_source`: source to suppress
- `add_source`: source to add
- `depth`: shorter, normal, or deeper
- `priority_delta`: raise or lower a source's priority

For dynamic source discovery, propose candidates with:

- name
- URL
- category
- why it matches the user's interests
- expected signal/noise risk
- whether it should be `candidate` or `personal`

Ask before adding candidates to persistent config.

## Scheduling guidance

This skill does not install schedules by itself.

If the user's agent supports reminders, cron, or scheduled jobs, create the schedule using that agent's native scheduler. The scheduled job should run an agent turn that uses this skill and then deliver the resulting briefing through the agent's normal channel.

Avoid hardcoded chat IDs, personal tokens, or provider-specific message-sending commands in shared skill files.

## Validation

A briefing is complete when:

- it covers the requested time window
- source links are present
- duplicates are collapsed
- top items include practical implications
- failures or gaps are disclosed briefly
- any persistent source changes are proposed, not silently applied

## Common failure modes

- **Feed URL fails:** try the website's alternate RSS/Atom URL, then continue.
- **Too many generic items:** tighten categories and raise thresholds for actionability.
- **Too much AI hype:** prefer primary docs, technical writeups, and credible analysts over summaries.
- **Paid newsletter content:** link and summarize only publicly available metadata unless the user provides private content for personal use.
- **Source drift:** periodically review muted/noisy sources and candidate sources.
