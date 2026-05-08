# AGENTS Entry Point

Use with The Documenter when creating, refreshing, or auditing `AGENTS.md`.

`AGENTS.md` is not a second README. It is the operational contract for coding agents working in the repo.

## Identity

Write `AGENTS.md` for a careful engineering agent:

- Think before editing.
- State assumptions when repo evidence is incomplete.
- Prefer the simplest working change.
- Keep edits surgical.
- Match existing repo style.
- Define success criteria before implementation.
- Verify with repo-supported commands.

## Evidence To Inspect

- Current `AGENTS.md`, if present
- `CLAUDE.md`, only to confirm it points to `AGENTS.md`
- `README.md` and `docs/README.md`
- Project manifests and lockfiles
- Build/test/lint scripts
- Entry points and runtime config
- CI/deploy config
- Module docs and source layout
- Existing formatting/code style config

## Required AGENTS.md Shape

Include these sections when repo evidence supports them:

1. Project Purpose
2. Build + Run
3. Architecture
4. Entry Points
5. Conventions
6. Formatting Rules
7. Code Style Rules
8. File Placement
9. Before Editing
10. Change Discipline
11. Migrations / Scripts
12. Domain Notes / Feature Notes
13. Verification
14. Known Gotchas

Keep sections terse and operational. Use tables for commands and file maps.

## Before Editing Section

Include a section based on these rules:

- Do not assume. Inspect first.
- If multiple interpretations exist, name them and ask or choose the least risky repo-consistent path.
- If a simpler approach solves the request, use it.
- If requirement is unclear enough to risk wrong work, stop and ask.
- Identify files likely to change before editing.
- Keep every changed line traceable to the user's request.

## Change Discipline Section

Include a section based on these rules:

- Minimum change that solves the task.
- No speculative features.
- No new abstraction for one use.
- No unrelated refactors, formatting churn, or cleanup.
- Match existing style even if another style seems better.
- Remove only dead code created by the current change.
- Mention unrelated issues instead of editing them.

## Goal-Driven Verification Section

For each repo-supported command, document purpose and when to run it.

Use this style for complex tasks:

```text
1. Inspect affected files -> verify: source of truth found
2. Make smallest scoped edit -> verify: diff only touches requested area
3. Run repo checks -> verify: documented commands pass
```

Do not invent verification commands. If repo has no tests, say so plainly.

## Commands Table

Use exact commands from repo evidence:

| Command | Purpose | When To Run |
|---|---|---|
| `command` | | |

## File Map Table

Map where agents should work:

| Area | Path | Notes |
|---|---|---|
| Runtime entry | `path` | |
| Tests | `path` | |
| Config | `path` | |

## CLAUDE.md Rule

If `CLAUDE.md` exists, keep it pointer-only:

```markdown
# CLAUDE.md

See [AGENTS.md](./AGENTS.md) for agent instructions.
```

Do not duplicate AGENTS content in `CLAUDE.md`.

## Writing Rules

- Use imperatives.
- Be terse and concrete.
- Prefer repo-specific rules over generic guidance.
- Omit unsupported facts.
- Do not include motivational language.
- Do not explain basic programming concepts.
- Do not document secrets.
- Do not repeat README content except where agents need operational detail.

## Frontend Additions

When used with `frontend-entrypoint.md`, include frontend-specific agent rules:

- package manager and exact scripts
- routing model
- app bootstrap entry
- component/hook/screen placement
- state/API/auth boundaries
- styling/theme conventions
- form/validation conventions
- test/lint/typecheck commands
- mobile native caveats, if applicable

## Backend Additions

When used with `backend-entrypoint.md`, include backend-specific agent rules:

- build/run commands
- solution/project/module map
- host startup path
- request lifecycle/middleware
- controller/service/repository conventions
- DTO naming and placement
- DI/registration rules
- database/migration rules
- API/auth rules
- external integration rules
- deployment doc link only, no runbook duplication

## Verification

Before shipping `AGENTS.md`:

1. Every command appears in repo evidence.
2. Every cited path exists.
3. `AGENTS.md` and repo README agree on shared facts.
4. `CLAUDE.md` is pointer-only.
5. Rules are specific enough to guide edits.
6. Rules do not ask agents to refactor or expand scope by default.
7. No secrets or secret values are included.
