# TODO

## Publication Checklist

- [x] Review the two public example source domains for privacy concerns.
- [x] Recreate the empty `wiki/` directory.
- [x] Add `/coding-preferences-improve`, manual-by-default Git rules, and permission-request explanations.
- [x] Ingest and lint `3d-printing-example`.
- [x] Ingest and lint `communication-example`.
- [x] Verify current wiki links, tags, source coverage, and activity logs.
- [x] Check whether `CODING-PREFERENCES.md` still contains its exact generic starter text; restore it if needed.
- [x] Review every public file, including the final README, rules, commands, example raw notes, and compiled wiki.
- [x] Simplify the README command reference and remove redundant command-catalog notices.
- [x] Restart OpenCode to load the changed command files.
- [x] Run `/maintenance` after the documentation and catalog changes.
- [x] Run `git init` manually.
- [x] Review `git status`, then manually stage and commit the reviewed files.
- [ ] Re-add lines in gitignore
- [ ] Add GNU GPL v3.0 and update related documentation after the first commit.
- [ ] Create the public GitHub repository and push only after reviewing the first commit.

## Future Work

Insert here your todos to work on them later.

OpenCode may add, update, or remove TODO items only after asking for and receiving explicit user permission.

## Manual Git Rules

- By default, the agent only shows `git add`, `git commit`, `git push`, `git checkout`, and `git switch` commands for you to type.
- It runs those commands only if you explicitly authorize automatic Git actions for the current session.
- That authorization does not persist to later sessions.

## Permission Explanation Rule

Before every permission prompt, including prompts offering Allow, Allow all, or Deny, the agent states one line:
`Permission request: <action and target> - <reason>.`

For conversational permission prompts, the available choices are: Allow once, Allow all for this session, Deny, and Ask info about <action>. The built-in OpenCode permission UI has fixed options and cannot add a fourth button through project configuration.
