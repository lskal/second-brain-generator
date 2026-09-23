---
description: Runs readme-sync, commands-list-sync, and meta-check as one maintenance bundle
agent: build
---
Propose the maintenance scope and request explicit confirmation before running these commands in sequence. Follow each file exactly; do not reinterpret its steps:

1. @.opencode/commands/readme-sync.md
2. @.opencode/commands/commands-list-sync.md
3. @.opencode/commands/meta-check.md

After the initial confirmation, do not ask for an additional maintenance-level confirmation between steps. Honor any confirmation required by an invoked command before it writes a file.

After each step, give a one- or two-line summary. Consolidate applicable manual Git suggestions into one command, for example `git add -A && git commit -m "chore: periodic maintenance"`; omit it if nothing was written. Do not run it. End with an overall summary and any `meta-check` item needing manual attention.
