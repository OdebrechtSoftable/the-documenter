# AGENTS.md

Operational guide for agents working in Sample Frontend.

## Build + Run

| Command | Purpose | When To Run |
|---|---|---|
| `npm install` | Install dependencies | Fresh checkout |
| `npm run dev` | Start Vite dev server | Local UI work |
| `npm run build` | Production build | Before shipping frontend changes |
| `npm run lint` | Lint frontend code | Before handoff |

## Architecture

```text
src/main.tsx -> src/App.tsx -> src/pages/* -> src/hooks/* -> src/services/api/*
```

## Conventions

- Use `src/pages/` for route-level views.
- Use `src/components/` for reusable UI.
- Use `src/hooks/` for data and UI state hooks.
- Use `src/services/api/` for HTTP calls.

## Formatting Rules

- Follow `eslint.config.js`.
- Keep imports consistent with nearby files.
- Avoid formatting-only diffs.

## Code Style Rules

- Components use PascalCase.
- Hooks start with `use`.
- API functions return typed data.
- UI states include loading, empty, and error handling.

## File Placement

| Work Type | Path |
|---|---|
| Route | `src/pages/` |
| Component | `src/components/` |
| Hook | `src/hooks/` |
| API client | `src/services/api/` |

## Before Editing

- Inspect route, component, hook, and API layer before editing behavior.
- Confirm scripts in `package.json`.
- Keep change scoped to requested flow.

## Verification

| Command | Purpose |
|---|---|
| `npm run lint` | Lint |
| `npm run build` | Build |
