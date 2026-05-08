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
