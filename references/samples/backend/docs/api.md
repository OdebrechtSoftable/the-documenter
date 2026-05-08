# API

API documentation sample for an ASP.NET Core backend.

## Swagger / OpenAPI

Swagger is exposed in development when configured by the API host.

## Authentication

| Requirement | Source |
|---|---|
| Bearer token | Auth middleware configuration |

Do not document token values.

## Controller Map

| Controller | Base Path | Purpose |
|---|---|---|
| `AccountsController` | `/accounts` | Account reads |
| `OrdersController` | `/orders` | Order reads and status updates |

## DTO Locations

| Area | Path |
|---|---|
| Account DTOs | `src/Accounts/Dtos/` |
| Order DTOs | `src/Orders/Dtos/` |

## Error Shape

```json
{
  "message": "Validation failed",
  "errors": []
}
```

## Database Notes

Order endpoints read from PostgreSQL through repository classes.

## Related Docs

- [Architecture and Walkthrough](./architecture-and-walkthrough.md)
- [Testing](./testing.md)
