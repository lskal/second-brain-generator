---
description: Deletes wiki/<domain> or all wiki domains after three explicit confirmations; never touches raw/
agent: build
---
WARNING: this command deletes data. Follow these steps exactly in order. Never run the deletion before Step 6.

Requested target: `$ARGUMENTS`
- If empty, ask for an existing domain or explicit `all`. Do not assume `all`.
- Require `wiki/` itself to be a non-symlink directory before resolving any target.
- If the target is not literal `all`, accept it only when it matches `^[a-z0-9]+(-[a-z0-9]+)*$`. Reject every other value, including values containing `/`, `\\`, `.`, `..`, whitespace, or shell metacharacters.
- For a domain target, enumerate the direct child directories of `wiki/` and require an exact match. The matched directory must not be a symlink. Target only that direct child directory.
- Literal `all` targets the whole `wiki/`, including `wiki/index.md` and `wiki/log.md`.
- Otherwise stop and request a valid target.
- After validation, set `$target` to `wiki` for `all`, or to `wiki/<domain>` for a domain. Use this exact resolved target for every later listing, status check, and deletion; never use the raw argument as a path.

Never touch `raw/`, `README.md`, `AGENTS.md`, or `.opencode/`. Stop and report any operation that could affect them.

## Step 1: Show What Would Be Deleted
Run `find -- "$target" -type f | sort` and show the complete list and count. Do not continue until the user has seen it.

## Step 2: Check Git Status
Run `git status --porcelain`. If it is non-empty, stop and tell the user to commit before proceeding. Do not continue until the repository is clean.

## Step 3: Explain Recovery
State: "After deletion, wiki/<target> can be rebuilt with `/ingest <domain>` from `raw/`, but manually enriched or lint-corrected concept pages must be regenerated. This is not an automatic restore." For `all`, state this for every domain.

## Step 4: First Confirmation
Ask: "To confirm, type this exact target name: $ARGUMENTS". Continue only on an exact case-sensitive match.

## Step 5: Second Confirmation
Ask: "Type the exact phrase CONFIRM WIPE to continue." Continue only on that exact case-sensitive response.

## Step 6: Final Confirmation and Deletion
Show the Step 1 list and count again. Ask: "Final confirmation: I will now run `rm -rf -- <target>`. Type YES to continue." Run `rm -rf -- "$target"` only after exact case-sensitive `YES`.

## After Deletion
Do not run Git write commands. Suggest the manual command `git add -A && git commit -m "wipe: <target>, <date>"` so the operation can be recovered with `git revert`. Confirm deletion and give exact rebuild commands for every touched domain.

If the target was not `all`, append `## [YYYY-MM-DD] wipe | <target> | Domain deleted; rebuild with /ingest` to surviving `wiki/log.md`. For `all`, skip this because the log was deleted.


At any step, stop if the response is not exact. Never interpret ambiguous replies as confirmation.
