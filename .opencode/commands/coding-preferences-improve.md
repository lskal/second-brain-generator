---
description: Proposes targeted improvements to an existing personalized CODING-PREFERENCES.md
agent: build
---
This command manages only the repository-root `CODING-PREFERENCES.md`. If `$ARGUMENTS` is not empty, stop and explain that custom paths are not supported.

Require `CODING-PREFERENCES.md` to be a non-symlink regular file before reading or writing.

## Step 1: Read the Current State

Read `CODING-PREFERENCES.md` if it exists.

- If it is missing, empty, contains only the starter onboarding message, or records that the user chose not to personalize preferences, stop. Recommend `/coding-preferences` instead.
- Otherwise, treat it as an existing personalized preference file. Preserve its stated preferences unless the user explicitly changes them.

## Step 2: Propose Improvements, No Writes

Ask what the user wants to improve. If their goal is already clear from the conversation, do not ask again.

Review the file for concrete gaps, ambiguities, contradictions, or outdated guidance that relate to that goal. Do not infer preferences from a role, project, or common practice. Summarize the proposed changes and ask any essential clarifying question before drafting.

## Step 3: Draft and Confirm

Show a complete revised Markdown file. Ask: "Write this to <target path>? Reply YES to confirm or describe changes."

Do not write before exact `YES`. Do not run Git commands.
