---
description: Finds terms cited inline in 2+ pages without their own page and promotes confirmed candidates
agent: build
---
IMPORTANT: use `grep`, never `rg`/`ripgrep`; `grep` is guaranteed available.

If `$ARGUMENTS` is empty, stop and ask for `<domain>`. Do not assume one.

Require the domain name to match `^[a-z0-9]+(-[a-z0-9]+)*$` and to be an exact, non-symlink direct child directory of `wiki/`. Reject path separators, `.`, `..`, whitespace, shell metacharacters, and unknown domains before reading or writing.

## Step 1: Scout, No Changes

Find technical terms or concepts cited inline in 2+ `wiki/$ARGUMENTS/concepts/` pages without a dedicated concept page, using the criterion in `AGENTS.md`. List each citing page with line references.

Use the judgment in `AGENTS.md`: exclude bibliography and terms that lose meaning outside mapping or comparison tables. Still report them as "cited 2+ times, promotion discouraged" with the reason.

Number each promotable candidate.

## Step 2: Request Explicit Confirmation

Ask: "Which candidates should be promoted? Reply with numbers, 'all recommended', or 'none'." Do not create pages without an explicit response. Clarify ambiguous replies rather than assuming they include discouraged candidates.

## Step 3: Apply Only Approved Candidates

For each approved candidate, follow the concept-page rules in `AGENTS.md`: create a dedicated page in `wiki/$ARGUMENTS/concepts/`, consolidate existing cited content into it, replace duplicates with links, apply taxonomy tags, and update incoming links from source pages and the domain index.

Leave unapproved and discouraged candidates inline and unchanged.

Verify touched new and modified pages with `wc -l` before and after.

Append `## [YYYY-MM-DD] lint-fix | $ARGUMENTS | Promoted N concepts from scouting: <names>` to `wiki/log.md`.

## Commit Suggestion

If any candidate was promoted, end with: `Manual Git command: git add -A && git commit -m "docs($ARGUMENTS): promote N concepts"`. Do not run it.

## Recommended Next Step

If Step 3 promoted any candidate, end with: "Recommended next step: `/lint $ARGUMENTS`" to check incoming links, tags, and new candidates.
