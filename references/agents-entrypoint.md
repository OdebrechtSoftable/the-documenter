# AGENTS Entry Point

Use with The Documenter when creating, refreshing, or auditing `AGENTS.md`.

`AGENTS.md` is not a second README. It is the operational contract for coding agents working in the repo.

## Required Opening Block

Every `AGENTS.md` file in every repo being documented must start with this block before any repo-specific title or instructions:

```markdown
1. Think Before Coding
Don't assume. Don't hide confusion. Surface tradeoffs.

Before implementing:

State your assumptions explicitly. If uncertain, ask.
If multiple interpretations exist, present them - don't pick silently.
If a simpler approach exists, say so. Push back when warranted.
If something is unclear, stop. Name what's confusing. Ask.
2. Simplicity First
Minimum code that solves the problem. Nothing speculative.

No features beyond what was asked.
No abstractions for single-use code.
No "flexibility" or "configurability" that wasn't requested.
No error handling for impossible scenarios.
If you write 200 lines and it could be 50, rewrite it.
Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

3. Surgical Changes
Touch only what you must. Clean up only your own mess.

When editing existing code:

Don't "improve" adjacent code, comments, or formatting.
Don't refactor things that aren't broken.
Match existing style, even if you'd do it differently.
If you notice unrelated dead code, mention it - don't delete it.
When your changes create orphans:

Remove imports/variables/functions that YOUR changes made unused.
Don't remove pre-existing dead code unless asked.
The test: Every changed line should trace directly to the user's request.

4. Goal-Driven Execution
Define success criteria. Loop until verified.

Transform tasks into verifiable goals:

"Add validation" → "Write tests for invalid inputs, then make them pass"
"Fix the bug" → "Write a test that reproduces it, then make it pass"
"Refactor X" → "Ensure tests pass before and after"
For multi-step tasks, state a brief plan:

1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.
```

Repo-specific content must come after this block.

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

## Code Format Style Pointer

`AGENTS.md` is not the source of truth for code formatting and style. `docs/code-format-patterns-style.md` is.

The Formatting Rules, Code Style Rules, and File Placement sections must:

1. Summarize the highest-leverage rules in under ~15 lines each (package manager, lint/format/typecheck commands, the 3-5 most important conventions).
2. End with this pointer line:

```markdown
See [docs/code-format-patterns-style.md](./docs/code-format-patterns-style.md) for the full code format, patterns, and style reference.
```

Do not duplicate the full style ruleset, anti-pattern tables, or extended code examples in `AGENTS.md`. If a contributor needs more than the summary, they follow the pointer.

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

1. The required opening block is the first content in the file.
2. Every command appears in repo evidence.
3. Every cited path exists.
4. `AGENTS.md` and repo README agree on shared facts.
5. `CLAUDE.md` is pointer-only.
6. Rules are specific enough to guide edits.
7. Rules do not ask agents to refactor or expand scope by default.
8. Formatting Rules, Code Style Rules, and File Placement sections each end with a pointer to `docs/code-format-patterns-style.md`; full style ruleset is not duplicated in `AGENTS.md`.
9. No secrets or secret values are included.
