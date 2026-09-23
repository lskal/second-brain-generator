---
description: Lints one domain or the whole wiki and confirms proposed fixes before applying them
agent: build
---
IMPORTANT: use `grep`, never `rg`/`ripgrep`; `grep` is guaranteed available.

If `$ARGUMENTS` is empty, ask for a domain or explicit `all`. Do not assume `all`.

Require `wiki/` itself to be a non-symlink directory. For a domain argument, require `^[a-z0-9]+(-[a-z0-9]+)*$` and an exact, non-symlink direct child directory of `wiki/`; for `all`, enumerate only non-symlink direct child directories. In every selected domain, require existing `concepts/` and `sources/` directories, index files, and `wiki/log.md` to be non-symlink paths before reading or writing. Reject path separators, `.`, `..`, whitespace, shell metacharacters, unknown domains, and symlinked paths.

SESSION WARNING: if this session already ran `/ingest`, `/lint`, `/brain-status`, or `/domain-close`, warn that context accumulates. Ask the user to check the OpenCode context indicator and consider `/exit` and a new session. Do not block the operation.

## Step 1: Analysis, No Changes

For `all`, run the Lint operation in `AGENTS.md` for every domain. Otherwise run it only for `$ARGUMENTS`.

Check contradictions, orphan pages, concepts missing their own page (the 2+ page criterion, with mapping-table judgment), and inconsistent frontmatter. Validate `tags`, `stack`, and `topics` against `AGENTS.md`. Number every finding and propose its resulting action.

Treat `not-verifiable` and `unresolved` as terminal statuses under `AGENTS.md`. Do not automatically downgrade either to `needs-verification`; propose a status change only with concrete evidence that the situation changed.

If no fixes are needed, state that explicitly and propose appending a `lint` entry to `wiki/log.md`: this is a clean lint. Do not append it before the confirmation in Step 2.

## Step 2: Request Explicit Confirmation

If proposals exist, ask: "What should I apply? Reply with numbers (for example, '1,3'), 'all', or 'none'." Do not apply anything without an explicit response. If no fixes are needed, ask: "Record this clean lint in wiki/log.md? Reply YES to confirm or no to leave the log unchanged." Do not append the entry without exact `YES`.

## Step 3: Apply Only Approved Proposals

Apply only confirmed items. Report unapproved ones as "not applied on request". Update `wiki/log.md`: use `lint` after a confirmed clean lint and `lint-fix` when at least one fix was applied, listing the changes.

## Commit Suggestion

End with `Manual Git command: git add -A && git commit -m "lint-fix($ARGUMENTS): <short fix list>"` if a fix was applied, or `Manual Git command: git add -A && git commit -m "lint($ARGUMENTS): no fixes needed"` for a clean lint. Do not run it.

## Recommended Next Step

Suggest only applicable follow-ups:
- Suggest `/checklist-sync` after changing any `needs-verification`, `not-verifiable`, or `unresolved` status.
- Suggest `/readme-sync` when this changes the number of complete domains.
- Count `wiki/log.md` entries with `grep -c "^## \["`; if divisible by 5, suggest `/maintenance`, but never run it automatically.
