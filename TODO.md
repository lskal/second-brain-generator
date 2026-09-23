# TODO

## Suggested First Steps

- [ ] Read `README.md` and `AGENTS.md` before adding knowledge. `raw/` notes are immutable after ingestion, and personal content must stay private.
- [ ] Explore `3d-printing-example` and `communication-example` as public references, or remove them if they are not useful to you.
- [ ] Review `.gitignore` and confirm new personal domains under `raw/` and `wiki/` will remain untracked.
- [ ] Create a personal domain in `raw/<domain>/` and add Markdown source notes.
- [ ] Run `/ingest <domain>` and explicitly approve the proposed source scope.
- [ ] Review the generated `wiki/<domain>/sources/`, `concepts/`, and `index.md` pages in Obsidian.
- [ ] Run `/lint <domain>` and choose which proposed corrections to apply.
- [ ] Run `/maintenance` after ingesting or linting to refresh status and check project documentation.

## Optional Setup

- [ ] Run `/coding-preferences` to personalize collaboration preferences.
- [ ] Run `/commands-list-sync` after adding or changing project commands.
- [ ] Initialize or connect Git only when you want version control for your own changes.

## Future Work

Add your own tasks here as your knowledge base grows.

OpenCode may add, update, or remove TODO items only after asking for and receiving explicit user permission.

## Manual Git Rules

- By default, the agent only shows `git add`, `git commit`, `git push`, `git checkout`, and `git switch` commands for you to type.
- It runs those commands only if you explicitly authorize automatic Git actions for the current session.
- That authorization does not persist to later sessions.

## Permission Explanation Rule

Before every permission prompt, including prompts offering Allow, Allow all, or Deny, the agent states one line:
`Permission request: <action and target> - <reason>.`

For conversational permission prompts, the available choices are: Allow once, Allow all for this session, Deny, and Ask info about <action>. The built-in OpenCode permission UI has fixed options and cannot add a fourth button through project configuration.
