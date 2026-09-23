---
description: Ingests all unprocessed sources in a domain, or specified source files, after confirmation
agent: build
---
IMPORTANT: use `grep`, never `rg`/`ripgrep`; `grep` is guaranteed available.

Arguments use `/ingest <domain> [raw-file ...]`.

If `$ARGUMENTS` is empty, list the direct child directories of `raw/` and ask the user to choose a domain. Do not assume one.

If a domain is supplied without filenames, scope the operation to every unprocessed source in that domain. If filenames follow the domain, scope it only to those exact files in `raw/<domain>/`; reject names outside that directory.

Before reading or writing, require the domain name to match `^[a-z0-9]+(-[a-z0-9]+)*$` and to be an exact, non-symlink direct child directory of `raw/`. Every selected raw source must be a regular, non-symlink file directly in that domain. Require `wiki/` itself to be a non-symlink directory. If `wiki/<domain>/` already exists, it must be an exact, non-symlink direct child; if absent, create only that direct directory after scope confirmation. Existing `sources/` and `concepts/` directories must be non-symlinks; create missing ones only as direct children of `wiki/<domain>/`. Existing domain indexes and `wiki/log.md` must be non-symlink regular files before updating. Recheck every destination immediately before writing. Reject path separators, `.`, `..`, whitespace, shell metacharacters, and unknown domains.

SESSION WARNING: if this session already ran `/ingest`, `/lint`, `/brain-status`, or `/domain-close`, warn that context accumulates. Ask the user to check the OpenCode context indicator and consider `/exit` and a new session. Do not block the operation.

## Step 1: Proposal, No Writes

Compare normalized names in `raw/<domain>/` and `wiki/<domain>/sources/` to find un-ingested sources in the requested scope. List them. For more than 10 files, propose batches of 5-8 grouped by topic or relation.

For more than 3 batches (about 20 files), warn that automatic context compaction can lose detail or fail. Recommend at most 2-3 batches per invocation, then rerun `/ingest $ARGUMENTS` for remaining files.

If nothing needs ingesting, report it and stop.

## Step 2: Request Explicit Confirmation

Ask: "Ingest these N files in M batches? Reply YES to proceed, state a batch limit (for example, 'YES, first 2 batches only'), or list files to exclude." Do not start without an explicit response. End this turn with that question only; give no follow-up recommendation until Step 3 completes.

## Step 3: Run One Batch at a Time

Run the Ingest operation in `AGENTS.md`, one batch at a time. After every batch:
1. Verify its source and concept pages exist on disk.
2. Immediately append that batch's entry to `wiki/log.md`.
3. Report the completed batch and continue with the next approved batch.

If a batch limit was agreed, stop there and clearly report remaining files.

If the user exits during a batch, it may be partial. On the next `/ingest $ARGUMENTS`, inspect the affected source and concept pages, report the state, and ask whether to complete or replace the partial batch before continuing.

After all planned batches, compare normalized source names for the entire domain and report any remaining un-ingested files.

## Recommended Next Step

After Step 3, always end with: "Recommended next step: `/lint <domain>`". If raw and sources match, report ingest completion. If batches remain, report their count and advise rerunning `/ingest <domain>`.

Count `wiki/log.md` entries with `grep -c "^## \["`. If the count is divisible by 5, suggest `/maintenance`; never run it automatically.

Do not run Git commands. If a Git repository exists, a user may choose to commit completed work separately.
