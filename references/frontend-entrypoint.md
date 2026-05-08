# Frontend Entry Point

Use with The Documenter for frontend web, mobile, and UI repos.

Target repos include React, Next.js, Vite, React Native, Expo, browser apps, mobile apps, design systems, component libraries, and user-facing dashboards.

## Evidence To Inspect

- `package.json`
- Lockfile: `package-lock.json`, `pnpm-lock.yaml`, `yarn.lock`
- App directories: `src/`, `app/`, `pages/`, `components/`, `hooks/`, `features/`, `screens/`, `routes/`
- Asset/style dirs: `public/`, `assets/`, `styles/`, `theme/`, `globals/`
- Config: `vite.config.*`, `next.config.*`, `app.json`, `app.config.*`, `tsconfig.json`, `eslint.*`, `prettier.*`, `babel.config.*`, `metro.config.*`
- Safe env/config examples: `.env.example`, safe `.env*` names, Expo public config
- Auth/client API layers
- Routing files
- State/context/store files
- CI/deploy/preview config
- Existing docs under `docs/` and feature folders

## Required Frontend Facts

Document only repo-backed facts:

- package manager
- framework/runtime
- app bootstrap entry point
- routing model
- state management model
- API client layer
- auth/session handling
- component structure
- screen/page placement
- styling/theming system
- forms/validation approach
- assets/static file handling
- accessibility or responsive constraints
- build/export/preview flow
- test/lint/typecheck scripts
- mobile native build flow, if Expo/React Native

## Repo README Shape

Keep root `README.md` concise:

- what app does
- framework/runtime
- local setup
- install command
- dev/start command
- build command
- test command, if present
- lint/format/typecheck command, if present
- env/config names without secret values
- folder layout summary and major challenges
- link to `docs/README.md`
- link to `docs/deployment.md` for deploy/preview flow, if applicable
- known issues/difficulties
- license/versioning
- owner/support path

Do not put route maps, component catalogs, design deep dives, API maps, or deployment runbooks in root `README.md`.

## Frontend Docs

Create or refresh these docs when evidence supports them:

- `docs/commercial-overview.md`: nontechnical overview of product functionality, workflows, and business impact.
- `docs/core-concepts/*`: domain concepts, glossary, features, use cases.
- `docs/architecture-and-walkthrough.md`: route -> screen/page -> hook/context -> API/client -> UI flow.
- `docs/DESIGN.md`: design system, user-facing terminology, layout rules, responsive behavior, accessibility.
- `docs/testing.md`: test/lint/typecheck commands, manual smoke checks, known gaps.
- `docs/deployment.md`: static export, preview, app store, EAS, CI/CD, or hosting flow when present.
- `docs/README.md`: docs hub and reading path.

## AGENTS.md Frontend Shape

Use `agents-entrypoint.md` for common agent rules, then add frontend-specific rules below.

Put operational content once in `AGENTS.md`:

- package manager
- exact scripts
- app bootstrap entry point
- routing model
- file placement rules
- component, hook, screen, and context naming
- state and API boundaries
- auth/client token rules
- styling/theming conventions
- form/validation conventions
- test/lint/typecheck rules
- mobile native build caveats, if applicable
- before-editing checks
- verification commands

`CLAUDE.md` remains pointer-only to `AGENTS.md`.

## Verification

Before shipping frontend docs:

1. Run documented finite commands: install only if needed, build, lint, typecheck, tests when present.
2. Smoke-start documented dev/start command until boot is visible, then stop.
3. Confirm package manager from lockfile/package scripts.
4. Confirm route model from actual route dirs/files.
5. Confirm API/auth docs from actual client/interceptor/provider files.
6. Confirm `docs/DESIGN.md` matches existing style/theme/components.
7. Confirm deployment docs live in `docs/deployment.md`, not root `README.md`.
8. Confirm no secret values are documented.
