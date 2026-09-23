---
description: Runs ingest and lint for one domain with a token warning and explicit confirmation
agent: build
---
If `$ARGUMENTS` is empty, stop and ask for `<domain>`. Do not assume one.

Require the domain name to match `^[a-z0-9]+(-[a-z0-9]+)*$` and to be an exact, non-symlink direct child directory of both `raw/` and `wiki/`. Reject path separators, `.`, `..`, whitespace, shell metacharacters, and unknown domains before reading or writing.

## Step 0: Warning and Confirmation

Before doing anything, warn: "This command runs /ingest and /lint for the entire $ARGUMENTS domain in one session. Multiple ingest batches or many concept pages can consume significant context and tokens. Use a model with a large token budget. If this session already ran heavy commands, check the OpenCode context indicator and consider `/exit` and a new session. Type YES to continue; any other response cancels."

Proceed only if the response is exactly `YES` (case-sensitive). Otherwise cancel without changes.

## Step 1: Ingest

After confirmation, run `@.opencode/commands/ingest.md` for `$ARGUMENTS`, including batching when required.

## Step 2: Lint

Immediately run `@.opencode/commands/lint.md` for the same domain. Preserve its propose-confirm-apply flow: its confirmation is separate from Step 0.

## Final Summary

Give one summary of ingested sources, touched concept pages, lint findings, and applied fixes. Include each applicable follow-up suggestion only once. Consolidate manual Git suggestions into one command, for example: `git add -A && git commit -m "domain-close($ARGUMENTS): ingest + lint"`. Do not run it.
