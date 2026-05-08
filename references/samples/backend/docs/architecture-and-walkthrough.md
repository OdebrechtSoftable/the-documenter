# Architecture and Walkthrough

## Overview

Sample Backend is an ASP.NET Core API. It exposes account and order endpoints for frontend clients.

## Runtime Flow

```text
HTTP request -> auth middleware -> controller -> service -> repository -> PostgreSQL -> response
```

## Key Modules

| Module | Purpose | Key Paths |
|---|---|---|
| API host | Runtime startup | `SampleApi/Program.cs` |
| Accounts | Account read model | `src/Accounts/` |
| Orders | Order behavior | `src/Orders/` |
| Shared | Cross-cutting code | `src/Shared/` |

## Key Files

| Path | Why It Matters |
|---|---|
| `SampleApi/Program.cs` | Registers middleware, services, and API host |
| `SampleApi/Controllers/OrdersController.cs` | Order endpoints |
| `src/Orders/Services/OrderService.cs` | Order business behavior |
| `src/Orders/Repositories/OrderRepository.cs` | Order database access |

## Request / Event Lifecycle

1. Request reaches ASP.NET Core host.
2. Auth middleware validates bearer token.
3. Controller validates request shape.
4. Service applies domain behavior.
5. Repository reads or writes PostgreSQL.
6. Controller returns response DTO.

## Operational Gotchas

- Local run requires database config.
- API docs must match actual controllers and DTOs.
