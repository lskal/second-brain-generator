---
description: Finds pages with a given tags, stack, or topics value and reports the reason
agent: build
---
IMPORTANT: use `grep`, never `rg`/`ripgrep`; `grep` is guaranteed available.

If `$ARGUMENTS` is empty, ask for `<value>` such as `needs-verification`, `unresolved`, `react`, or `macos`. Do not continue.

Search all concept pages for `$ARGUMENTS` in frontmatter `tags`, `stack`, or `topics`:

```
grep -rlE "^(tags|stack|topics):.*\b$ARGUMENTS\b" wiki/*/concepts/
```

For each page, report:
- Its explicit reason, if stated.
- Otherwise, a clearly labeled hypothesis based on the page content.
- The matching field: `tags`, `stack`, or `topics`.

Do not modify files. Group results by domain and provide a total.

For a status value (`resolved`, `in-progress`, `needs-verification`, `not-verifiable`, or `unresolved`), apply the scope in `AGENTS.md`. Flag apparent misuse for review without correcting it automatically.
