# AGENTS.md

Operational guide for agents working in Sample Backend.

## Build + Run

| Command | Purpose | When To Run |
|---|---|---|
| `dotnet build SampleApi.sln` | Build solution | Before backend handoff |
| `dotnet run --project SampleApi/SampleApi.csproj` | Start API | Local API smoke |

## Architecture

```text
request -> middleware -> controller -> service -> repository/integration -> response
```

## Entry Points

| Area | Path | Notes |
|---|---|---|
| Host | `SampleApi/Program.cs` | API startup |
| Controllers | `SampleApi/Controllers/` | HTTP endpoints |
| Services | `src/*/Services/` | Domain behavior |
| Repositories | `src/*/Repositories/` | Database access |

## Conventions

- Controllers stay thin.
- Services own business behavior.
- Repositories own data access.
- DTOs define request and response contracts.

## Formatting Rules

- Follow existing C# formatting.
- Keep one public class per file.
- Avoid formatting-only diffs.

## Code Style Rules

- Interfaces start with `I`.
- Controllers end with `Controller`.
- Services end with `Service`.
- Repositories end with `Repository`.

## File Placement

| Work Type | Path |
|---|---|
| Controller | `SampleApi/Controllers/` |
| Service | `src/<Domain>/Services/` |
| Repository | `src/<Domain>/Repositories/` |
| DTO | `src/<Domain>/Dtos/` |

## Migrations / Scripts

- Confirm migration flow from repo files before adding migrations.
- Do not invent database commands.

## Verification

| Command | Purpose |
|---|---|
| `dotnet build SampleApi.sln` | Compile backend |

## Known Gotchas

- Local API start requires database connectivity.
- Do not document secret connection string values.
