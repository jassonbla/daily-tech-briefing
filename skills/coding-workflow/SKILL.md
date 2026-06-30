---
name: coding-workflow
description: Run coding tasks with a disciplined, PR-oriented agent workflow. Use when the user asks to implement, debug, refactor, review, or investigate code changes and the work benefits from scope framing, repository context, isolated worktrees or worker agents, validation, and concise evidence-based reporting.
license: MIT
metadata:
  version: "1.0.0"
  checklist: references/checklist.md
---

# Coding Workflow

Use this skill for coding work that should be handled as a disciplined engineering task rather than an ad-hoc chat edit. The workflow emphasizes clear scope, fresh repository context, safe isolation, implementation toward a reviewable diff, validation evidence, and explicit reporting of what was checked versus left unchecked.

## When to use

Use this skill when the user asks to:

- implement a feature
- fix a bug
- refactor code
- investigate a regression
- prepare a PR-shaped change
- review or modify a multi-file code path
- coordinate one or more coding agents or worker sessions

Use a lighter approach for tiny one-file edits, pure explanations, or quick lookups where the overhead would not improve safety or quality.

## Operating principles

- Clarify ambiguity before expanding scope.
- Prefer evidence from the current repository over memory or assumptions.
- Keep risky or substantial changes isolated from the main working tree.
- Delegate substantial implementation work to isolated workers when the environment supports it.
- Validate with the cheapest meaningful checks first, then stronger checks when risk justifies them.
- Report the result in a form that would be useful for a code review.

## Workflow

### 1. Frame the task

Before editing, shape the request into a compact execution frame:

- Goal: what should be true when the task is done?
- Scope: which repo, app, package, feature, or file area is involved?
- Constraints: compatibility, release timing, style, safety, migration, or user-specified limits.
- Likely approach: implementation path or investigation hypothesis.
- Validation plan: tests, builds, lint, type checks, manual checks, screenshots, or logs.
- Parallelization: whether the work is one coherent task or several independent tracks.

If the target, range, success criteria, or safety boundary is unclear, ask one focused question instead of guessing.

### 2. Refresh repository context

When working in a git repository, inspect current state before changing files:

```bash
git status --short
git branch --show-current
git remote -v
git fetch origin --prune
```

Prefer the latest default branch or the user-specified base. Do not assume local branches are current.

If repository documentation, architecture notes, wiki pages, code indexes, or knowledge tools are available, inspect the relevant ones before broad text search. Use semantic/code-index tools when present for definitions, references, routes, API handlers, shared types, and impact checks. If those tools are unavailable, fall back to local file reads and targeted search.

### 3. Isolate the work

For fresh implementation tasks, prefer a clean worktree or branch from the intended base:

```bash
git worktree add <path> origin/main -b <task-branch>
```

Adjust the base branch to match the user's request. Reuse an existing worktree only for follow-up work on the same task.

Use direct edits in the current tree only when the change is small, low-risk, and the working tree is clean or already intentionally scoped.

### 4. Decide whether to delegate

Keep the main conversation as the control plane:

- clarify requirements
- split independent tracks
- assign focused worker scopes
- reconcile results
- summarize decisions and validation

Delegate substantial coding loops to isolated workers when available. Good worker briefs include:

- objective
- repo/worktree path and base branch
- files or areas in scope
- constraints and out-of-scope items
- expected validation commands
- deliverable: diff summary, tests run, risks, blockers

Parallelize independent tasks. Avoid parallelizing tightly coupled edits that require constant coordination.

### 5. Build context before editing

Before changing code, inspect the relevant implementation path:

- entry points, routes, commands, components, jobs, or handlers
- domain types and schemas
- existing patterns and nearby tests
- call sites, references, and shared utilities
- migration/deployment implications

For shared APIs or types, check downstream consumers before changing signatures or response shapes.

### 6. Implement toward a reviewable diff

Make the smallest coherent change that satisfies the goal. Prefer existing project conventions over new patterns. Keep unrelated cleanup out of the patch unless it directly reduces risk.

For changes involving user data, credentials, external sends, destructive operations, production config, migrations, or scheduler behavior, pause and confirm when the requested action is not explicit.

### 7. Validate

Run checks that match the change risk. Examples:

```bash
npm test
npm run lint
npm run typecheck
npm run build
pytest
cargo test
go test ./...
```

When full validation is too expensive or unavailable, run targeted checks and clearly state the limitation. If a check fails, distinguish between:

- failure caused by the patch
- pre-existing failure
- environment/tooling failure
- incomplete setup

### 8. Prepare review-ready output

A good final report includes:

- What changed
- Why it changed
- Files or areas touched
- Validation run and results
- What was not validated
- Risks, edge cases, or follow-up recommendations

Keep it concise, but include enough evidence that a reviewer can trust the status.

## Progress reporting

Use short, decision-useful checkpoints for longer tasks:

- Started and scope confirmed
- Root cause identified
- Implementation ready
- Tests passed
- Blocked and why
- Needs user decision

Avoid noisy narration for obvious steps. Report when there is a meaningful state change or decision point.

## Code search guidance

Prefer precise search over broad scans:

```bash
rg "symbolOrRouteName" path/to/repo
rg --files | rg "component|module|service"
git grep "GraphQLFieldName"
```

Use broad repository scans only when the target is unclear and narrower methods failed. If search stops converging, ask for clarification instead of guessing.

## Safety notes

- Do not run destructive commands without explicit approval.
- Prefer reversible file moves over permanent deletion.
- Do not expose secrets from config, environment files, logs, or credentials.
- Inspect existing config before modifying it; merge rather than clobber.
- Ask before posting externally, opening PRs, deploying, or changing production state.
- Treat generated code and dependency changes as supply-chain risk until reviewed.

## Decision guide

Use this skill strongly when:

- the task spans multiple files or systems
- the user expects implementation, not just advice
- the work could become a pull request
- correctness depends on repository context
- validation evidence matters
- independent subtasks can be delegated or parallelized

Use a lighter approach when:

- the user only wants a quick explanation
- the change is a trivial one-file edit
- no repository mutation is needed
- delegation overhead would exceed the task size
