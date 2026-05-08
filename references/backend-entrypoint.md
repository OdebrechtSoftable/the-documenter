# Backend Entry Point

Use with The Documenter for backend, API, service, worker, and data-processing repos.

Target repos include .NET APIs, ASP.NET Core services, background workers, REST APIs, GraphQL APIs, queue consumers, integration services, and persistence-heavy backend systems.

## Evidence To Inspect

- Solution/project files: `.sln`, `.csproj`, package manifests
- Host startup: `Program.cs`, `Startup.cs`, app host/bootstrap files
- Config: `appsettings*.json`, safe `.env*` names, Docker/config manifests
- API surface: controllers, minimal APIs, routes, GraphQL schemas, OpenAPI/Swagger config
- Domain/service/repository layers
- DTO/request/response contracts
- Data access: EF migrations, migration scripts, SQL/Dapper files, ORM config
- Auth/authorization middleware and policies
- External integration clients
- Dockerfiles and compose files
- CI/deploy config
- Existing docs under `docs/` and module folders

## Required Backend Facts

Document only repo-backed facts:

- runtime and framework
- solution/project layout
- host/entry point
- build/run commands
- API docs/Swagger/OpenAPI flow
- auth model and required headers
- request lifecycle or middleware pipeline
- controller/endpoint/module map
- service/domain/repository boundaries
- DTO/request/response locations
- database and migration flow
- error response shape
- pagination/filtering conventions, if present
- external integrations
- deployment/Docker flow links
- test/build verification commands

## Repo README Shape

Keep root `README.md` concise:

- what API/service does
- runtime/framework
- local setup
- build/run commands
- database and migration summary
- Swagger/OpenAPI or API docs link
- env/config names without secret values
- Docker summary, if present
- link to `docs/README.md`
- link to `docs/deployment.md` for deployment flow, if applicable
- known issues/difficulties
- license/versioning
- contribution notes

Do not put full endpoint maps, DTO catalogs, migration runbooks, integration internals, or deployment runbooks in root `README.md`.

## Backend Docs

Create or refresh these docs when evidence supports them:

- `docs/commercial-overview.md`: nontechnical business functionality and impact.
- `docs/core-concepts/*`: domain concepts, glossary, features, use cases.
- `docs/architecture-and-walkthrough.md`: request -> middleware -> controller/handler -> service -> repository/integration -> response flow.
- `docs/testing.md`: build/test commands, API smoke checks, DB prerequisites, known gaps.
- `docs/deployment.md`: CI/CD, Docker, environment, release, smoke, rollback flow.
- API docs under `docs/` when Swagger/OpenAPI or route maps need explanation.
- Module docs under `docs/` for large domains.
- `docs/README.md`: docs hub and reading path.

## AGENTS.md Backend Shape

Use `agents-entrypoint.md` for common agent rules, then add backend-specific rules below.

Put operational content once in `AGENTS.md`:

- build and run commands
- base branch/source-of-truth rules
- solution/project/module inventory
- request lifecycle or middleware pipeline
- key files
- domain/service/repository conventions
- DTO naming and placement
- DI/registration rules
- database/migration rules
- external integration rules
- formatting/code style rules
- file placement rules
- deployment doc link, without duplicating deployment runbook
- verification commands

`CLAUDE.md` remains pointer-only to `AGENTS.md`.

## API Docs Shape

Document API facts from repo evidence:

- Swagger/OpenAPI URL or generation flow
- auth model and required headers
- role/permission requirements
- base paths and controller/module map
- request and response DTO locations
- error response shape
- pagination/filtering conventions
- DB transaction/migration rules affecting API behavior
- external integrations used by endpoints
- safe example requests from repo docs/tests only

Do not document secret values or private credentials.

## .NET-Specific Checks

When repo is .NET-based, confirm:

- actual `.sln` and `.csproj` names
- target framework
- host project
- `Program.cs` / `Startup.cs` runtime flow
- DI registration location
- EF migration location and command flow, if present
- Swagger/OpenAPI config
- targeted build command vs full solution build guidance
- test project presence or absence

## Verification

Before shipping backend docs:

1. Run documented finite commands: build, tests, lint/format where present.
2. Smoke-start documented run command only when external services/secrets are not required.
3. Confirm API docs match actual controllers/endpoints/Swagger config.
4. Confirm migration docs match actual migrations/scripts.
5. Confirm config/env docs name variables only, never values.
6. Confirm deployment docs live in `docs/deployment.md`, not root `README.md`.
7. Confirm `AGENTS.md` has operational backend rules and `CLAUDE.md` is pointer-only.
