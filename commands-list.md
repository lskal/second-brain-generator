# OpenCode Commands

## Daily Work

`/ingest <domain>`
What it does: Proposes and ingests unprocessed raw sources for one domain in confirmed batches.
When to use it: Use after adding or changing immutable source notes in `raw/<domain>/`.
Example: `/ingest 3d-printing-example`

`/lint <domain|all>`
What it does: Checks wiki pages for contradictions, orphaned concepts, missing concepts, and invalid frontmatter.
When to use it: Use after ingesting a domain or when reviewing wiki quality.
Example: `/lint communication-example`

`/brain-status`
What it does: Reports each domain's raw-source, ingest, and lint status with ready commands.
When to use it: Use to see what work remains across the wiki.
Example: `/brain-status`

## Diagnostics and Maintenance

`/tags <tag|stack|topic>`
What it does: Finds pages with a requested `tags`, `stack`, or `topics` value and reports why they match.
When to use it: Use to inspect how a classification value is used.
Example: `/tags resolved`

`/orphans <domain|all>`
What it does: Finds concept pages without incoming links and proposes confirmed link repairs.
When to use it: Use after structural changes or a lint finding about orphans.
Example: `/orphans 3d-printing-example`

`/promote-candidates <domain>`
What it does: Finds concepts cited inline on two or more pages without their own page and proposes promotions.
When to use it: Use to grow a mature domain's reusable concept layer.
Example: `/promote-candidates communication-example`

`/checklist-sync`
What it does: Regenerates `verification-checklist.md` from concept-page verification statuses.
When to use it: Use after changing a concrete verification status.
Example: `/checklist-sync`

`/readme-sync`
What it does: Regenerates only the dynamic README status and verification-total blocks.
When to use it: Use after the number of complete domains or verification totals changes.
Example: `/readme-sync`

`/meta-check`
What it does: Reviews `README.md` and `AGENTS.md` for drift from the project workflow.
When to use it: Use before publication or periodic maintenance.
Example: `/meta-check`

## Other

`/coding-preferences`
What it does: Personalizes the repository-root `CODING-PREFERENCES.md` through a concise, role-aware interview.
When to use it: Use when the generic starter preferences need first-time personalization.
Example: `/coding-preferences`

`/coding-preferences-improve`
What it does: Proposes targeted, confirmed refinements to the repository-root personalized preferences file.
When to use it: Use when established preferences need a user-directed update.
Example: `/coding-preferences-improve`

`/domain-close <domain>`
What it does: Runs ingest and lint for one domain while preserving both confirmation flows.
When to use it: Use to complete a focused domain-maintenance cycle.
Example: `/domain-close 3d-printing-example`

`/maintenance`
What it does: Runs README synchronization, command-list synchronization, and metadata checking together.
When to use it: Use for periodic project housekeeping.
Example: `/maintenance`

`/pre-commit`
What it does: Reports commit readiness from domain status, metadata checks, and Git status.
When to use it: Use before manually staging a reviewed change set.
Example: `/pre-commit`

`/wipe <domain|all>`
What it does: Deletes a wiki domain or all wiki content only after three explicit confirmations.
When to use it: Use only when a wiki rebuild is intentional and raw sources remain available.
Example: `/wipe 3d-printing-example`

16 commands available in total (15 described above plus `/commands-list-sync` itself). See README.md for the command overview and AGENTS.md for shared command rules.
