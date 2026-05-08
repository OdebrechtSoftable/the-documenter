# Testing

## Overview

The sample project supports lint and production build checks. No E2E command exists in the sample repo.

## Commands

| Command | Purpose | Notes |
|---|---|---|
| `npm test` | Run tests | Use when test script exists |
| `npm run lint` | Run linter | Run before handoff |
| `npm run build` | Verify production build | Run before release-facing changes |

## Test Layers

| Layer | Location | Scope |
|---|---|---|
| Unit | `src/__tests__/` | Component and hook behavior |
| Manual smoke | Browser | App boot, navigation, API error state |

## Fixtures and Test Data

Fixture data lives under `src/__tests__/fixtures/` when present.

## Manual Smoke Checks

| Flow | Steps | Expected Result |
|---|---|---|
| App boot | Start dev server and open home page | Page renders without console errors |
| Orders | Open orders route with API available | Orders table renders or empty state appears |

## Known Gaps

No sample E2E command is documented.
