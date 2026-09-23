---
description: Reports every domain's raw, ingest, and lint status with ready-to-run fixes
agent: build
---
IMPORTANT: use `grep`, never `rg`/`ripgrep`; `grep` is guaranteed available.

For each domain in `raw/<domain>/`, do not only count files. Compare normalized filenames file by file:

```
diff <(ls raw/<domain>/ | sed 's/\.md$//; s/_/-/g' | tr '[:upper:]' '[:lower:]' | sort) \
     <(ls wiki/<domain>/sources/ | sed 's/\.md$//; s/_/-/g' | tr '[:upper:]' '[:lower:]' | sort)
```

Resulting `<` lines may be missing source pages; `>` lines are source pages without matching raw files. Before reporting a gap, apply the known exceptions from `AGENTS.md` and `wiki/log.md`:
- Consolidated sources.
- Sources intentionally ingested in another domain.
- Cross-domain sources whose raw file lives elsewhere.
- Report only unexplained `<` lines, by filename. Explained `>` lines are normal.

For lint status, search `wiki/log.md` for both `lint` and `lint-fix`; both count as completed. Compare the latest result with the latest ingest.

**Use this exact Bash date comparison:**

```bash
last_ingest=$(grep -E "^## \[[0-9-]+\] ingest \| $domain \|" wiki/log.md | sed 's/^## \[//; s/\].*//' | sort | tail -1)
last_lint=$(grep -E "^## \[[0-9-]+\] lint(-fix)? \| $domain \|" wiki/log.md | sed 's/^## \[//; s/\].*//' | sort | tail -1)
domain_state=complete
if [[ -n "$last_ingest" ]] && { [[ -z "$last_lint" ]] || [[ "$last_lint" < "$last_ingest" ]]; }; then
  domain_state=lint
fi
```

Avoid `[ "$a" \< "$b" ]`; use `[[ "$a" < "$b" ]]`. Do not name a variable `status`, which is read-only in zsh; use `domain_state`.

Present a summary table: domain | raw sources | source pages | status (complete / ingest needed + files / lint needed).

## Ready Commands

For every incomplete domain, immediately follow the table with the exact applicable command:

To fix <domain>: run /ingest <domain>
To fix <domain>: run /lint <domain>

If both are needed, write two lines in order: ingest, then lint.

Omit this section if all domains are complete.

## Recommended Next Step

Always end with: "Recommended next step: `/meta-check`". It checks whether the project handoff documentation needs updating after recent activity.
