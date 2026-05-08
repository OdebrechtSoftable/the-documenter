# Sample Backend

.NET Web API for account and order data used by commercial applications.

## Table of Contents

- [Documentation](#documentation)
- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [Repository Layout](#repository-layout)
- [Local Development](#local-development)
- [Environment Variables / Configuration](#environment-variables--configuration)
- [Database and Migrations](#database-and-migrations)
- [API Docs](#api-docs)
- [Known Issues / Difficulties](#known-issues--difficulties)
- [License and Versioning](#license-and-versioning)

## Documentation

See [docs/README.md](./docs/README.md) for the full documentation map.

Deployment details: [docs/deployment.md](./docs/deployment.md).

## Tech Stack

| Area | Technology |
|---|---|
| Runtime | .NET |
| Framework | ASP.NET Core |
| Language | C# |
| Database | PostgreSQL |

## Architecture

ASP.NET Core API. Controllers receive HTTP requests, services apply domain behavior, repositories access the database, and integrations live behind clients.

## Repository Layout

```text
.
|-- SampleApi/
|-- src/
|   |-- Accounts/
|   `-- Orders/
`-- docs/
```

| Path | Purpose |
|---|---|
| `SampleApi/Program.cs` | API host bootstrap |
| `src/Accounts/` | Account domain |
| `src/Orders/` | Order domain |
| `docs/` | Detailed documentation |

## Local Development

| Command | Purpose |
|---|---|
| `dotnet build SampleApi.sln` | Build solution |
| `dotnet run --project SampleApi/SampleApi.csproj` | Start API |

## Environment Variables / Configuration

| Name | Required | Purpose |
|---|---:|---|
| `ConnectionStrings__Default` | Yes | PostgreSQL connection string name |

Do not include secret values.

## Database and Migrations

Migrations live under `SampleApi/Migrations/`.

## API Docs

Swagger is available when the API runs in development.

## Known Issues / Difficulties

- API start requires database connectivity.
- Integration clients require environment-specific config names.

## License and Versioning

Version is maintained in project metadata. License source is repo license file.
