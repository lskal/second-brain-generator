---
description: Checks orphan pages without incoming links in one domain or all domains, with confirmed fixes
agent: build
---
IMPORTANT: use `grep`, never `rg`/`ripgrep`; `grep` is guaranteed available.

If `$ARGUMENTS` is empty, ask for a domain or explicit `all`. Do not assume `all`.

For a domain argument, require `^[a-z0-9]+(-[a-z0-9]+)*$` and an exact, non-symlink direct child directory of `wiki/`. Reject path separators, `.`, `..`, whitespace, shell metacharacters, and unknown domains before reading or writing.

## Step 1: Report, No Changes

For `all`, check each domain. Otherwise check only `$ARGUMENTS`.

This is only the orphan-page portion of Lint.

A page is orphaned when no other wiki page (concept, source, or index) references it with a `[[...]]` link. Exclude self-references, `wiki/log.md`, and root project documentation.

For each orphan, number it and report domain, page name, a hypothesis for why it is unlinked, and a concrete incoming-link proposal. Do not force weak links.

End with: domain | orphan pages | total domain pages.

If none exist, report it and stop.

## Step 2: Request Explicit Confirmation

If proposals exist, ask: "Add the proposed links? Reply with numbers, 'all', or 'none'." Do not modify anything without an explicit response.

## Step 3: Apply Only Approved Links

For each approved page, add the incoming wikilink at the proposed point, or a better point found on review and explain why. Do not change the rest of that page. Verify with `wc -l` before and after.

If any link was applied, append `## [YYYY-MM-DD] lint-fix | <domain> | Linked N orphan pages: <names>` to `wiki/log.md`; for `all`, add one entry per touched domain.

## Commit Suggestion

If any link was applied, end with: `Manual Git command: git add -A && git commit -m "docs($ARGUMENTS): link N orphan pages"`. Do not run it.

## Recommended Next Step

If any link was applied, end with: "Recommended next step: `/lint $ARGUMENTS`".
