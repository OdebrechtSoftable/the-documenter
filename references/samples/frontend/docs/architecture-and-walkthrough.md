# Architecture and Walkthrough

## Overview

Sample Frontend is a React + Vite app. It renders client-side pages and reads backend data through a shared API client.

## Runtime Flow

```text
browser -> src/main.tsx -> src/App.tsx -> page -> hook -> API client -> UI state
```

## Key Modules

| Module | Purpose | Key Paths |
|---|---|---|
| Bootstrap | Mount React app | `src/main.tsx` |
| Pages | Route-level screens | `src/pages/` |
| Hooks | Data loading and local state | `src/hooks/` |
| API client | Backend requests | `src/services/api/` |
| Components | Shared UI | `src/components/` |

## Request Lifecycle

1. Page renders.
2. Page calls a hook.
3. Hook calls API function.
4. API client attaches base URL and auth header.
5. Hook maps response to loading, success, empty, or error state.
6. Page renders the matching UI state.

## Operational Gotchas

- `VITE_API_BASE_URL` must be configured for API requests.
- Keep route pages thin; move reusable behavior into hooks or components.
