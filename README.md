# Second Brain Generator

A local-first personal knowledge base built with Markdown, Obsidian, and an AI coding agent. It follows Andrej Karpathy's [LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) pattern: raw notes are immutable inputs; an agent compiles them into an interlinked wiki.

## How It Works

```text
README.md               # project overview and workflow
AGENTS.md               # rules for agents and wiki maintenance
CODING-PREFERENCES.md   # optional personalized collaboration preferences
commands-list.md        # generated command catalog
TODO.md                 # permission-gated task list
raw/<domain>/           # immutable source notes
wiki/<domain>/          # generated and maintained knowledge pages
  concepts/             # reusable concepts
  sources/              # one summary per raw source
  index.md              # domain map
wiki/index.md           # global map
wiki/log.md             # append-only activity log
```

Keep domains separate by default. Add a cross-domain link only when the relationship is genuinely useful, and explain it in a dedicated section.

### A Local RAG-Like Workflow

This project applies the practical idea behind Retrieval-Augmented Generation (RAG) locally. `raw/` contains the source material; when asked to ingest a source, the agent reads the relevant files, extracts useful context, and writes a structured, linked wiki in `wiki/`. The generated pages become a maintained knowledge layer that is easier for both people and the agent to navigate than the original notes alone.

It is not a conventional production RAG system: there are no embeddings, vector database, automatic semantic retrieval, or per-question context injection into a model. Retrieval is deliberate and file-based: the agent reads the requested source pages and connected wiki pages for the task at hand. This keeps the vault local, inspectable, and Markdown-first while preserving the core RAG principle of grounding generated material in source context.

## Getting Started

1. Install [OpenCode](https://opencode.ai) and [Obsidian](https://obsidian.md).
2. Choose the model that best fits your needs and available access. This project was developed with GPT-5.6 Terra by OpenAI. You can also use models through OpenRouter, an OpenCode membership plan such as Go, or OpenAI directly. OpenCode does not recommend using an Anthropic subscription with this product.
3. Open this folder as an Obsidian vault and as an OpenCode project.
3.5. `3d-printing-example` and `communication-example` are public example domains. You can use them as references or remove them at your discretion; keep personal knowledge-base domains private by default.

Git is optional. The knowledge base and its OpenCode workflows work with or without an initialized Git repository. Initialize Git only when you want version control or intend to publish the project.

4. Create a domain in `raw/<domain>/` and add Markdown notes. Treat a note as immutable once it enters `raw/`.
5. You can also export a past Claude or ChatGPT conversation with the prompt in [Importing External Chat Context](#importing-external-chat-context), then place the generated Markdown in the appropriate `raw/<domain>/` directory.
6. Run `/ingest <domain>` in OpenCode. It proposes work before writing pages.
7. Open `wiki/<domain>/index.md` in Obsidian and run `/lint <domain>` when the domain is mature.

Restart OpenCode after changing `opencode.json`, `.opencode/commands/`, or `.opencode/skills/`.

## Vault Status

<!-- AUTO-GENERATED:quick-status -->
Last checked: 2026-09-23 - 2/2 domains complete (ingest + lint).

| Domain | Raw sources | Source pages | Status |
|---|---:|---:|---|
| `3d-printing-example` | 2 | 2 | complete |
| `communication-example` | 1 | 1 | complete |
<!-- END-AUTO:quick-status -->

Run `/readme-sync` after ingesting or linting to refresh this local status. Review the generated domain names before publishing the README, because they can reveal private vault structure.

## Vault Next Actions

<!-- AUTO-GENERATED:next-actions -->
No ingest or lint actions are pending.
<!-- END-AUTO:next-actions -->

## Importing External Chat Context

To bring an existing Claude or ChatGPT conversation into the vault, run the following reusable prompt directly in that conversation. It asks the external chat to produce one or more Markdown source files ready for `raw/<domain>/`.

```text
Reread this conversation and determine whether it covers one or more distinct topics or projects. If it covers more than one, create a separate Markdown file for each topic (not a single file with mixed sections). For each file—intended as a source for a personal knowledge management system—include: 1) the topic or project being discussed and why; 2) the key decisions made and the reasoning behind them (not just the final outcome); 3) technical terms or project-specific proper nouns useful for understanding future references; 4) any errors or approaches that were discarded and why; 5) the date of the chat (approximate if not exact—if it cannot be inferred from the text, check any screenshots or media attached to the chat for visible dates); 6) a final section with 3–7 free-form tags in the #tag format covering the file’s main content. Give each file a clear H1 title that identifies the topic. Omissions: no sensitive data (credentials, third-party personal data, specific financial information, private URLs, internal hostnames, ticket identifiers, or proprietary code). Write in [Italian/English depending on the language of the original chat], in clear prose, avoiding excessive bulleted lists. Don’t limit yourself to just a few lines; be as clear and informative as possible. The output should be a downloadable Markdown file.
```

Before placing the generated files in `raw/<domain>/`, verify that each file actually belongs to that domain. A plausible filename is not enough. Move or regenerate files that do not match the target domain before running `/ingest`.

## Public Example Domains

The repository includes two complete, safe domains in the normal vault structure:

- `raw/3d-printing-example` and `wiki/3d-printing-example`: Italian source notes compiled into English pages about Bambu Studio process presets and Plane Cut.
- `raw/communication-example` and `wiki/communication-example`: Italian public-speaking course notes compiled into English wiki pages.

All other domains under `raw/` and `wiki/` are ignored by Git on purpose. Copy an example domain to begin, but keep your real knowledge base private by default.

## OpenCode Commands

Project commands live in `.opencode/commands/`. Run `/commands-list-sync` for the complete local command catalog.

## Privacy

Do not put credentials, client data, private URLs, internal hostnames, ticket identifiers, proprietary code, or personal information in raw notes that you intend to publish. An agent can summarize and redact information, but it cannot replace a deliberate review of the source material.

`CODING-PREFERENCES.md` starts with a generic onboarding message. If you personalize it, review the changes before publishing them.

Git write commands are manual by default. OpenCode will show `git add`, `git commit`, `git push`, `git checkout`, and `git switch` commands for you to run unless you explicitly authorize automatic Git actions for the current session.

`TODO.md` is a local task list. OpenCode may update it only after asking for and receiving your explicit permission.

This repository has no license. Use it as inspiration for your own private knowledge base.
