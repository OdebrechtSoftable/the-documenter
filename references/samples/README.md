# Sample Project

Sample Project is a small React app that helps commercial users review account activity and order status.

## Table of Contents

- [Documentation](#documentation)
- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [Repository Layout](#repository-layout)
- [Local Development](#local-development)
- [Environment Variables / Configuration](#environment-variables--configuration)
- [Known Issues / Difficulties](#known-issues--difficulties)
- [License and Versioning](#license-and-versioning)
- [Contributing](#contributing)
- [Modules / Features at a Glance](#modules--features-at-a-glance)
- [Contacts / Ownership](#contacts--ownership)

## Documentation

See [docs/README.md](./docs/README.md) for the full documentation map.

Deployment details live in [docs/deployment.md](./docs/deployment.md).

## Tech Stack

| Area | Technology |
|---|---|
| Runtime | Node.js |
| Framework | React |
| Language | TypeScript |
| Package manager | npm |

## Architecture

Client-side app. Pages call hooks, hooks call the API client, and reusable UI lives under `src/components/`.

## Repository Layout

```text
.
|-- src/
|   |-- components/
|   |-- hooks/
|   |-- pages/
|   `-- services/
|-- docs/
`-- package.json
```

| Path | Purpose |
|---|---|
| `src/pages/` | Route-level UI |
| `src/services/` | API client code |
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

- Local dev needs a reachable backend API.
- Preview builds require `VITE_API_BASE_URL`.

## License and Versioning

Version is maintained in `package.json`. License source is the repo license file.

## Contributing

Run documented checks before handoff and keep detailed docs under `docs/`.

## Modules / Features at a Glance

| Module / Feature | Purpose | Docs |
|---|---|---|
| Account Activity | Review recent account updates | [Commercial Overview](./docs/commercial-overview.md) |
| Orders | Review order status by account | [Order Management](./docs/modules/order-management.md) |

## Contacts / Ownership

Owner or support path should be repo-backed or user-confirmed.
