# API

API notes for Sample Project.

## Overview

The frontend reads account and order data from the backend API through `src/services/api/client.ts`.

## Authentication

| Requirement | Source |
|---|---|
| Bearer token header | `src/services/api/client.ts` |

Do not document token values.

## Base Configuration

| Name | Required | Source | Purpose |
|---|---:|---|---|
| `VITE_API_BASE_URL` | Yes | `.env.example` | Backend base URL |

## Route Map

| Area | Method | Path | Client File |
|---|---|---|---|
| Accounts | `GET` | `/accounts` | `src/services/api/accounts.ts` |
| Orders | `GET` | `/orders` | `src/services/api/orders.ts` |

## Response Shape

```json
{
  "data": [],
  "meta": {
    "total": 0
  }
}
```

## Error Handling

API errors are normalized by `src/services/api/client.ts` before reaching UI hooks.

## Related Docs

- [Architecture and Walkthrough](./architecture-and-walkthrough.md)
- [Testing](./testing.md)
