---
description: Regenerates verification-checklist.md from concept-page frontmatter
agent: build
---
Read the current state of all wiki concept pages and identify pages tagged `needs-verification`, `not-verifiable`, or `unresolved`.

Compare the results with `verification-checklist.md`:

- Add pages that are in the results but absent from the checklist, including their stated reason when available.
- Move pages that are no longer in the results to a `Closed` section; do not silently delete them.
- Leave unchanged entries alone unless their status or stated reason changed.

Update the top counter so it exactly matches the current results. Do not modify concept pages. Write only `verification-checklist.md` after the user confirms the proposed changes.

If the checklist changed, recommend `/readme-sync` when the README contains a matching status summary. Do not run Git commands.
