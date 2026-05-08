# Deployment

Evidence-backed deployment runbook for Sample Project.

## Overview

Sample Project builds a static frontend artifact from `npm run build` and publishes `dist/` through the configured CI workflow.

## Build Artifact

| Artifact | Source Command / File | Output |
|---|---|---|
| Static frontend | `npm run build` | `dist/` |

## Environments

| Environment | Target | Notes |
|---|---|---|
| Preview | CI preview target | Used for review builds |
| Production | Static hosting target | Used for released app |

## Configuration

| Name | Required | Source | Purpose |
|---|---:|---|---|
| `VITE_API_BASE_URL` | Yes | `.env.example` | API base URL |

Do not include secret values.

## CI/CD Flow

1. Push change to deployment branch.
2. CI installs dependencies.
3. CI runs `npm run build`.
4. CI publishes `dist/` to configured target.

## Manual Deploy

No manual deploy command is documented in this sample repo.

## Release and Versioning

Version source is `package.json`.

## Smoke Checks

| Check | Command / URL | Expected Result |
|---|---|---|
| Build | `npm run build` | Build completes and writes `dist/` |
| Home route | Preview URL | Home page renders |

## Rollback / Recovery

Use the hosting provider rollback for the last successful static artifact.

## Known Issues

Preview build fails when `VITE_API_BASE_URL` is missing.
