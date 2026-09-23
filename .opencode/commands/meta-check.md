---
description: Reviews README.md and AGENTS.md for drift from the current project workflow
agent: build
---
Review `README.md`, `AGENTS.md`, `.opencode/commands/`, and recent `wiki/log.md` entries when present.

Report only these concrete gaps:

- A command exists but is not described in the README.
- A command conflicts with a rule in `AGENTS.md`.
- The README describes a workflow or file layout that no longer exists.
- A documented workflow has changed without a matching update to the README or `AGENTS.md`.

For each gap, cite the relevant files and propose concise replacement text. Do not write anything until the user explicitly approves selected proposals. Never invent a reason that cannot be established from the repository.

If no gap is found, state that the project documentation is consistent.
