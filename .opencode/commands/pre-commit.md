---
description: Reports commit readiness from brain-status, meta-check, and Git status
agent: build
---
IMPORTANT: use `grep`, never `rg`/`ripgrep`; `grep` is guaranteed available.

This command is read-only. Run in sequence:

1. `@.opencode/commands/brain-status.md`
2. `@.opencode/commands/meta-check.md`
3. `git status --porcelain`

Consolidate results into this report:

## Domain Status
(brain-status summary: N/M complete and ready commands for incomplete domains)

## Project Documentation
(meta-check summary: handoff documentation current or needing review)

## Git Worktree
(uncommitted changes grouped by `wiki/`, root project documentation, and `.opencode/commands/`)

## Verdict
End with "Ready to commit" if no domain is incomplete and `meta-check` has no critical issue. Uncommitted changes are normal. Otherwise write: "Before committing, consider: <short list>".

Never run `git add` or `git commit`; committing remains a separate manual action.
