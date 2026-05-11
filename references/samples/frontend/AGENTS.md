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
