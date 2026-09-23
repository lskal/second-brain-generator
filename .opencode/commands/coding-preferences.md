---
description: Personalizes CODING-PREFERENCES.md through a concise, role-aware interview
agent: build
---
This command manages only the repository-root `CODING-PREFERENCES.md`. If `$ARGUMENTS` is not empty, stop and explain that custom paths are not supported.

If `CODING-PREFERENCES.md` exists, require it to be a non-symlink regular file before reading or writing. If it does not exist, create only that repository-root path after the required confirmation.

## Step 1: Read the Current State

Read `CODING-PREFERENCES.md` if it exists.

- If it is empty, contains only the starter onboarding message, or records that the user chose not to personalize preferences, continue to Step 2.
- If it contains custom preferences, stop and do not overwrite it.

## Step 2: Choose Whether to Personalize

Ask: "Do you want to personalize coding preferences now? Reply `personalize`, `skip`, or `cancel`."

- `cancel`: stop without writing.
- `skip`: propose replacing the starter content with `The user chose not to personalize coding preferences.` Ask for exact `YES` before writing it, then stop.
- `personalize`: continue to Step 3.

## Step 3: Learn the Role and Environment

Ask for one or more roles: Frontend, Backend, Full-stack, DevOps, QA tester, or Other. Accept multiple selections. For Other, ask for the job or intended use.

Then ask only the relevant context: primary languages, frameworks or platforms, whether the work is modern, legacy, or mixed, and existing project conventions. Keep questions short and include inline generic examples, such as: "React or server-rendered templates", "modern or legacy", "follow the existing project", or "not sure".

## Step 4: Gather Useful Preferences

Ask small related groups of questions. Use generic inline examples and accept "not sure" without guessing.

- All roles: response style, verification, Git/review workflow, documentation, and actions that require explicit approval.
- Frontend: component/module structure, state scope, styling, accessibility, browser support, and refactoring tolerance. Examples: "keep it local", "use the project pattern", "smallest compatible change", or "improve nearby code only".
- Backend: API and data conventions, validation, errors, migrations, observability, and tests.
- Full-stack: applicable frontend and backend questions, plus boundaries, contracts, and end-to-end verification.
- DevOps: infrastructure, deployments, rollback, secrets, monitoring, incidents, and approval rules.
- QA tester: manual/automated testing, target platforms, bug reports, acceptance criteria, accessibility, regression, and release checks.
- Other: tools, files to maintain, risks, quality checks, and desired assistant behavior.

Ask follow-up questions only when an answer is ambiguous or changes the final preference file. Before drafting, summarize the captured context and ask whether anything important is missing.

## Step 5: Propose One File

Draft one complete but concise Markdown file with relevant sections from: `# Coding Preferences`, `## Roles and Context`, `## Working Style`, `## Implementation Practices`, `## Quality and Verification`, and `## Documentation and Collaboration`.

Show the complete draft and ask: "Write this to <target path>? Reply YES to confirm or describe changes." Do not write before exact `YES`. Do not run Git commands.
