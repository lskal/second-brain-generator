---
description: Regenerates the list and usage notes for all custom Second Brain commands
agent: build
---
IMPORTANT: use `grep`, never `rg`/`ripgrep`; `grep` is guaranteed available.

This command must not modify wiki pages, raw sources, or other project files. Step 3 may write only `commands-list.md`, the `command-summary` block in `README.md`, and `.commands-manifest.txt`, its internal cache file.

## Step 1: Cache Check

Determine every command's modification time cross-platform, including `commands-list-sync.md` itself so changes to this generator invalidate the cache. Try `stat -f '%N:%m' <file>` (macOS/BSD), then fall back to `stat -c '%n:%Y' <file>` (Linux/GNU):

```
find .opencode/commands -maxdepth 1 -name '*.md' -exec stat -f '%N:%m' {} \; | sort
```

If that fails, use:

```
find .opencode/commands -maxdepth 1 -name '*.md' -exec stat -c '%n:%Y' {} \; | sort
```

Compare the output with `.opencode/commands/.commands-manifest.txt`.

- **Exact match:** print `commands-list.md` and the `command-summary` block in `README.md` as-is without rereading command files, then stop.
- **Mismatch or either file missing:** continue to Step 2. This includes the first run.

## Step 2: Regenerate When the Cache Is Missing or Invalid

If Step 1 found a prior manifest, compare it line by line with current mtimes to identify which files changed:

- **Unchanged mtime:** do not reread it; reuse its existing `commands-list.md` entry.
- **Changed, new, or removed file:** always reread it in full and regenerate its entry from the current content.
- **No prior manifest:** reread every command file.

For multiple files to reread, use one combined shell call rather than separate reads. This changes only how they are read, not the requirement to read every changed file.

For each command being described, use this exact format. Keep the entire heading in one inline-code span so placeholders render correctly:

`/<name> <arguments when needed>`
What it does: <1-2 sentences from the actual command file>
When to use it: <1 practical sentence>
Example: `/<name> <example value>`

Leave one blank line between commands.

Group commands in this order, with each command appearing once:

## Daily Work
ingest, lint, brain-status

## Diagnostics and Maintenance
tags, orphans, promote-candidates, checklist-sync, readme-sync, meta-check

## Other
wipe, coding-preferences, and every command not listed above. New commands belong here until explicitly categorized.

At the end, count all `.md` files in `.opencode/commands/`, including `commands-list-sync.md`, and write: "N commands available in total (M described above plus /commands-list-sync itself). See README.md for the command overview and AGENTS.md for shared command rules." Use the real invokable total.

Also regenerate the `<!-- AUTO-GENERATED:command-summary -->` block in `README.md`. It must contain every command once in the same group order, including `/commands-list-sync`, with one Markdown bullet per command in this exact format:

```
- `/<name> <arguments when needed>`: <one concise sentence from the actual command file>
```

If either marker is missing, report it and do not create or guess its location.

## Step 3: Save the Cache

If Step 2 regenerated either output, show the proposed `commands-list.md` and README `command-summary` changes and request explicit confirmation before writing them and the current manifest to `.opencode/commands/.commands-manifest.txt`.

## Commit Suggestion

If Steps 2 and 3 regenerated the cache, end with: `Manual Git command: git add -A && git commit -m "chore: sync command catalogs"`. On a cache hit, no commit is needed. Do not run it.
