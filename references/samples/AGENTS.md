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

# AGENTS.md

Operational guide for agents working in Sample Project.

## Project Purpose

Sample Project is a React app that displays account activity from a backend API.

## Build + Run

| Command | Purpose | When To Run |
|---|---|---|
| `npm install` | Install dependencies | Fresh checkout or dependency change |
| `npm run dev` | Start local dev server | Local UI work |
| `npm run build` | Build production artifact | Before shipping UI changes |
| `npm run lint` | Run lint checks | Before final handoff |

## Architecture

```text
src/main.tsx -> src/App.tsx -> src/pages/* -> src/hooks/* -> src/services/api/*
```

State lives in React hooks and context. HTTP requests go through `src/services/api/client.ts`.

## Entry Points

| Area | Path | Notes |
|---|---|---|
| App bootstrap | `src/main.tsx` | React mount point |
| Routes | `src/pages/` | Page-level screens |
| API client | `src/services/api/client.ts` | Shared HTTP client |
| Theme | `src/styles/theme.ts` | Shared design tokens |

## Conventions

- Keep page files thin.
- Put reusable UI in `src/components/`.
- Put data loading hooks in `src/hooks/`.
- Do not call `fetch` directly from components.

## Formatting Rules

- Use repo lint rules from `eslint.config.js`.
- Keep existing import ordering.
- Avoid formatting-only diffs.

## Code Style Rules

- Components use PascalCase.
- Hooks start with `use`.
- API request and response types live beside API functions.
- Prefer explicit loading, empty, and error states.

## File Placement

| Work Type | Path |
|---|---|
| Page UI | `src/pages/` |
| Shared component | `src/components/` |
| API call | `src/services/api/` |
| Tests | `src/__tests__/` |

## Before Editing

1. Inspect affected files.
2. Confirm command support in `package.json`.
3. Choose smallest repo-consistent change.
4. Stop and ask if product behavior is ambiguous.

## Change Discipline

- No speculative features.
- No one-use abstraction.
- No unrelated refactors.
- Keep every changed line tied to the request.

## Migrations / Scripts

No database migrations exist in this sample frontend repo.

## Domain Notes / Feature Notes

- Account activity uses backend-provided status names.
- The UI does not invent status transitions.

## Verification

| Command | Purpose |
|---|---|
| `npm run lint` | Lint changed frontend files |
| `npm run build` | Verify production build |

## Known Gotchas

- Dev server needs `VITE_API_BASE_URL` configured.
- Do not document or commit secret values.
