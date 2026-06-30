# Example Worker Brief

```markdown
Task: Fix the settings page save regression.

Repo/worktree: `/path/to/repo-settings-fix`
Base: `origin/main`

Scope:
- Investigate settings save flow.
- Change only frontend form handling and directly related tests.
- Do not modify API contracts unless unavoidable; report first if needed.

Context to inspect:
- settings page component
- save mutation/client
- existing form tests
- recent commits touching settings

Validation expected:
- targeted settings tests
- typecheck if available

Deliverable:
- root cause
- diff summary
- tests run with results
- remaining risks or blockers
```
