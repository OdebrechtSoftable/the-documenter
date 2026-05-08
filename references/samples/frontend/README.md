# Sample Frontend

React frontend for reviewing account activity and order status.

## Table of Contents

- [Documentation](#documentation)
- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [Repository Layout](#repository-layout)
- [Local Development](#local-development)
- [Environment Variables / Configuration](#environment-variables--configuration)
- [Known Issues / Difficulties](#known-issues--difficulties)
- [License and Versioning](#license-and-versioning)

## Documentation

See [docs/README.md](./docs/README.md) for the full documentation map.

Deployment details: [docs/deployment.md](./docs/deployment.md).

## Tech Stack

| Area | Technology |
|---|---|
| Runtime | Node.js |
| Framework | React + Vite |
| Language | TypeScript |
| Package manager | npm |

## Architecture

Client-side React app. Routes render pages, pages call hooks, hooks call `src/services/api/`, and shared UI lives in `src/components/`.

## Repository Layout

```text
.
|-- src/
|   |-- components/
|   |-- hooks/
|   |-- pages/
|   `-- services/
|-- public/
`-- docs/
```

| Path | Purpose |
|---|---|
| `src/pages/` | Route-level UI |
| `src/services/api/` | API client layer |
| `src/components/` | Shared UI |
| `docs/` | Detailed documentation |

## Local Development

| Command | Purpose |
|---|---|
| `npm install` | Install dependencies |
| `npm run dev` | Start dev server |
| `npm run build` | Build production artifact |
| `npm run lint` | Run lint checks |

## Environment Variables / Configuration

| Name | Required | Purpose |
|---|---:|---|
| `VITE_API_BASE_URL` | Yes | Backend API base URL |

Do not include secret values.

## Known Issues / Difficulties

- Local dev requires a reachable backend API.
- Preview builds fail when `VITE_API_BASE_URL` is missing.

## License and Versioning

Version is maintained in `package.json`. License source is repo license file.
