---
description: Regenerates only the dynamic README.md blocks for quick status and verification totals
agent: build
---
IMPORTANT: use `grep`, never `rg`/`ripgrep`; `grep` is guaranteed available.

Update only content between `<!-- AUTO-GENERATED:... -->` and `<!-- END-AUTO:... -->` markers in `README.md`. Do not change anything else.

Before reading or writing, require repository-root `README.md` to be a non-symlink regular file. Stop if it is missing or a symlink.

Blocks to update:

1. **`quick-status`**: before calculating status, list all available domains and ask which domains may appear in the potentially tracked README. Default to the public example domains only; do not include any other domain without an explicit selection. Use the `brain-status` logic, including normalized raw/source comparison, its known exceptions, and equivalent `lint`/`lint-fix` outcomes. Use the exact date-comparison snippet from `brain-status.md`. Recount selected domains every run. Write: "Last checked: <today> - X/N selected domains complete (ingest + lint)." Then write a table with `domain`, `raw sources`, `source pages`, and `status`.

2. **`verification-summary`**: when this marker exists, count `needs-verification`, `unresolved`, and `not-verifiable` pages only across the selected domains, using the same logic as `/tags`. Write real counts as: "N `needs-verification`, N `unresolved`, N `not-verifiable`".

3. **`next-actions`**: list one ready command per incomplete selected domain, using `/ingest <domain>` before `/lint <domain>` when both are needed. When every selected domain is complete, write: "No ingest or lint actions are pending."

If a marker is missing, report it. Do not create one or guess its location.

Report changes from the previous values using real numbers. Before presenting a write confirmation, warn that selected domain names and status may be published with `README.md`. If a block would change, show the proposed replacement and request explicit confirmation before writing it.

## Commit Suggestion

If either block changed, end with: `Manual Git command: git add -A && git commit -m "chore: sync README status and verification totals"`. If neither changed, explicitly state that no commit is needed. Do not run it.
