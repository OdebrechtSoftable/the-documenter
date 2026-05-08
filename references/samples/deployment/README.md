# Deployment Folder

This sample represents a deployment or IaC folder README. Project deployment docs should still live in `docs/deployment.md`.

## Overview

The sample app builds a static artifact and deploys it through the repo CI workflow.

## Build Artifact

| Artifact | Source Command / File | Output |
|---|---|---|
| Static app | `npm run build` | `dist/` |

## CI/CD Flow

Push to the deployment branch runs the configured CI workflow, builds `dist/`, and publishes the artifact.

## Smoke Checks

| Check | Command / URL | Expected Result |
|---|---|---|
| Build | `npm run build` | Build completes |
