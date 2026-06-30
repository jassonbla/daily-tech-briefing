# Coding Workflow Checklist

## Before editing

- [ ] Confirm repo, branch/base, and task scope.
- [ ] Check `git status --short`.
- [ ] Fetch remote state if the task depends on current code.
- [ ] Inspect relevant docs, code index, or existing implementation patterns.
- [ ] Decide whether to use a branch/worktree or direct edit.

## During implementation

- [ ] Keep changes scoped to the task.
- [ ] Follow existing project conventions.
- [ ] Check call sites before changing shared APIs/types.
- [ ] Keep unrelated cleanup out unless it reduces immediate risk.
- [ ] Pause before destructive, external, production, credential, or scheduler changes.

## Validation

- [ ] Run targeted tests or checks for the changed area.
- [ ] Run broader lint/type/build checks when risk justifies them.
- [ ] Capture exact command results.
- [ ] Classify failures as patch-caused, pre-existing, environment, or setup-related.

## Final report

- [ ] Summarize what changed and why.
- [ ] Mention files or areas touched.
- [ ] List validation run and outcome.
- [ ] State what was not validated.
- [ ] Call out risks, edge cases, and follow-up actions.
