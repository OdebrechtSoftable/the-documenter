# The Documenter

The Documenter is an AI skill for creating and refreshing evidence-backed documentation for software projects.

It is designed for React, .NET, frontend, backend, API, service, and mixed repositories. The skill helps produce a practical documentation set without inventing commands, paths, environment variables, deployment steps, or workflows that are not supported by the repo.

## What It Creates

- Human-facing repo `README.md`
- `docs/README.md` documentation hub
- Module and feature docs
- `docs/core-concepts/` docs
- Commercial overview docs for nontechnical users
- Architecture and runtime walkthroughs
- Deployment docs outside the root README
- Testing docs
- API docs when supported by the repo
- Agent-focused `AGENTS.md`
- Pointer-only `CLAUDE.md`

## Skill Structure

```text
the-documenter/
|-- SKILL.md
`-- references/
    |-- README.md.template
    |-- deployment-README.md.template
    |-- architecture-and-walkthrough.md.template
    |-- DESIGN.md.template
    |-- testing.md.template
    |-- frontend-entrypoint.md
    |-- backend-entrypoint.md
    |-- agents-entrypoint.md
    |-- parallel-documentation-workflow.md
    |-- TODO.md
    `-- samples/
```

## Installation

To install this skill, prompt your AI coding agent to do it manually by creating the skill from this repository folder.

Example prompt:

```text
Install the skill from this folder as `the-documenter`.
Copy the folder contents into my skills directory so the skill can be loaded in future sessions.
Verify that `SKILL.md` and the `references/` folder are present after installation.
```

The target directory is usually:

```text
~/.codex/skills/the-documenter/
```

After installation, restart your AI tool so the new skill is picked up.

## Usage

Ask your AI coding agent to use The Documenter when creating, refreshing, auditing, or standardizing project documentation.

Example prompts:

```text
Use The Documenter to create documentation for this repo.
```

```text
Use The Documenter to refresh README, AGENTS, core concepts, deployment, and testing docs.
```

```text
Use The Documenter parallel workflow for this large repo.
```

## Core Rules

- Inspect repo evidence before writing.
- Never invent commands, paths, environment variables, deployment steps, owners, license, or versioning.
- Never document secret values.
- Keep root `README.md` concise and human-facing.
- Put detailed docs under `docs/`.
- Keep `CLAUDE.md` pointer-only to `AGENTS.md`.
- Run documented repo commands before shipping docs when possible.

## Parallel Workflow

For large repos, The Documenter uses a source-first workflow:

```text
repo evidence -> module docs -> core concepts -> shared facts -> parallel derived docs -> serial merge/verify
```

This keeps faster parallel doc writers grounded in module docs, core concepts, and a shared facts packet instead of raw partial context.
