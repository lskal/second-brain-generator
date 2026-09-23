# Second Brain Agent Rules

## Purpose

This is a local-first knowledge base using the LLM Wiki pattern. An agent reads immutable source notes and compiles them into a structured Markdown wiki that improves over time.

## Two Layers

- `raw/<domain>/`: immutable sources. Read them, never edit them.
- `wiki/<domain>/`: maintained Markdown pages for the user.

Each domain contains `concepts/`, `sources/`, and `index.md`. `wiki/index.md` maps all domains; `wiki/log.md` is the append-only global activity log.

`3d-printing-example` and `communication-example` are public demonstration domains. Do not treat them as a user's personal knowledge base or replace them during routine work.

## Language

Raw notes may remain in their original language. Generate all wiki pages in English by default, including pages derived from non-English raw notes. Keep established technical terms where they improve clarity.

## Ingest

When ingesting sources:

1. Identify the domain. If it is not specified, list the available domains in `raw/` and ask the user to choose one.
2. With a domain only, propose ingesting every unprocessed source in `raw/<domain>/`. With one or more source filenames, propose only those requested files.
3. Read only the sources in the approved scope. Never edit files in `raw/<domain>/`.
4. Create or update a page in `wiki/<domain>/sources/`.
5. Create or enrich relevant concept pages in `wiki/<domain>/concepts/`; link them with `[[wikilinks]]` rather than duplicating explanations.
6. Update the domain index and append `## [YYYY-MM-DD] ingest | <domain> | <source title>` to `wiki/log.md`.
7. Use a cross-domain link only for a strong conceptual relationship. Explain it under `## Cross-domain connections`.

## Naming

Keep raw filenames unchanged. Use lowercase kebab-case for source and concept pages. A different raw and wiki filename is expected when the source contains underscores, mixed case, or identifiers that should not appear in the wiki.

## Tags

Every concept page uses YAML frontmatter:

```yaml
---
tags: [pattern, resolved]
stack: [react]
topics: [accessibility]
---
```

`tags` must contain at least one type and exactly one status.

Types: `bug-fix`, `architecture`, `pattern`, `bibliographic-reference`.

Statuses: `resolved`, `in-progress`, `needs-verification`, `not-verifiable`, `unresolved`.

Use `needs-verification`, `not-verifiable`, and `unresolved` only for concrete code behavior or external facts. Stable educational material defaults to `resolved`.

`stack` is optional and contains framework or library names. `topics` is optional and contains kebab-case subject labels.

## Lint

On request, inspect the selected domain for contradictions, concept pages without incoming links, and substantial concepts mentioned in at least two pages without their own page. Propose corrections before writing. Log either `lint` or `lint-fix` when the operation completes.

## Privacy

Never copy credentials, personal data, private URLs, internal hostnames, ticket identifiers, or proprietary code into wiki pages. Generalize sensitive code and names. If publishing is intended, review raw sources separately: immutability does not make them safe to share.

## Verification

After modifying concept pages, run `wc -l` on the touched files and report the result. For frontmatter-only changes, inspect the diff instead.

## Command Rules

The slash commands in `.opencode/commands/` implement recurring workflows. Keep them consistent with this file. Commands that can write substantial content must propose the scope and request explicit confirmation before applying changes.

`/coding-preferences` personalizes `CODING-PREFERENCES.md` only after confirmation. The starter file is tracked, so users must review personalized changes before publishing them.

`/coding-preferences-improve` refines an existing personalized `CODING-PREFERENCES.md` only after confirmation. It must not invent preferences or overwrite the generic starter file.

`TODO.md` is a repository task list. Ask for and receive explicit user permission before adding, changing, or removing any TODO item.

## Git and Permissions

By default, show `git add`, `git commit`, `git push`, `git checkout`, and `git switch` commands for the user to run manually. Run one only when the user explicitly authorizes automatic Git actions for the current session; that authorization does not persist to later sessions.

Before every tool permission prompt, including prompts offering Allow, Allow all, or Deny, state exactly one preceding line: `Permission request: <action and target> - <reason>.` The action and target must be specific enough for the user to understand the requested access. Workflow confirmations, such as selecting lint proposals or typing an exact destructive-confirmation phrase, are not tool permission prompts and must state clearly what they approve.

For conversational permission prompts, offer: Allow once, Allow all for this session, Deny, and Ask info about <action>. If the user asks for information, explain the action and its scope before requesting a decision again. The built-in OpenCode permission UI has fixed options and cannot be extended with a fourth button through project configuration.
