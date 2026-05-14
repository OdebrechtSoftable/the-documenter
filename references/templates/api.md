# API — Template

Use this template for `docs/api.md` (or `docs/api/README.md` if the API surface is large enough to need a folder). Audience: engineers and agents who need to call the API or trace a request from UI to backend.

Evidence-first: every endpoint, header, env var, and response shape must come from a real file — controllers, route files, OpenAPI/Swagger config, axios clients, or fetcher modules. Never invent endpoints.

---

## Required Header

```markdown
# API

<one-sentence statement: which API this document describes, and which clients consume it>
```

If the repo consumes more than one API (e.g., internal API + third-party integrations), state the scope clearly and list each API as its own section. Do not mix routes across APIs in the same table.

---

## Section 1 — Overview

One paragraph + a Mermaid sequence diagram of a representative request.

```markdown
\`\`\`mermaid
sequenceDiagram
  participant Client
  participant Interceptor
  participant API
  Client->>Interceptor: request
  Interceptor->>API: request + auth header
  API-->>Interceptor: response
  Interceptor-->>Client: normalized data
\`\`\`
```

Cover: base URL source, client module path, transport (REST / GraphQL / gRPC), serialization format.

---

## Section 2 — Authentication

```markdown
| Requirement | Source |
|---|---|
| <header / token / cookie> | <file path> |
```

Rules:

- Document the auth mechanism (Bearer JWT, session cookie, API key, OAuth2 flow).
- Cite the interceptor or middleware that attaches credentials.
- Never document token values or secret credentials.
- If the API supports multiple auth methods, list all and state when each applies.

---

## Section 3 — Base Configuration

Environment variables the API client reads.

```markdown
| Name | Required | Source | Purpose |
|---|---:|---|---|
| `API_BASE_URL` | Yes | `.env.example` | Backend base URL |
```

Rules:

- Pull names from `.env.example` or repo config — never invent.
- Mark required vs. optional.
- Cite the source file where the variable is read.
- Never document values.

---

## Section 4 — Route Map

The canonical table. Every endpoint the client calls or the server exposes.

```markdown
| Area | Method | Path | Auth | Client File | Handler / Controller |
|---|---|---|---|---|---|
| Accounts | `GET` | `/accounts` | required | `src/services/api/accounts.ts` | `AccountsController.Get` |
| Orders | `POST` | `/orders` | required | `src/services/api/orders/post.ts` | `OrdersController.Create` |
```

Rules:

- Group rows by Area, alphabetical within group.
- Method always uppercase code-formatted.
- Path includes brace-style params: `/orders/{orderId}`.
- Auth column: `required` / `optional` / `public`.
- Client File required for frontend repos. Handler / Controller required for backend repos. Full-stack repos include both.
- If the API is too large for a single table (>50 endpoints), split into `docs/api/<area>.md` and link from `docs/api/README.md`.

---

## Section 5 — Request / Response Shapes

For each endpoint group, document the canonical request body and response. Pull types from the actual DTO files, not from hand-typed examples.

```markdown
### POST `/orders`

**Request body** — `src/dtos/orders/create-request.ts`:

\`\`\`json
{
  "customerId": "string",
  "items": [{ "sku": "string", "quantity": 0 }]
}
\`\`\`

**Response** — `src/dtos/orders/create-response.ts`:

\`\`\`json
{
  "orderId": "string",
  "status": "draft"
}
\`\`\`
```

Rules:

- Use JSON, not TypeScript types, for shape examples. Easier to scan, language-agnostic.
- Cite the DTO file or schema source above each block.
- Show the canonical happy-path shape. Edge cases go in Section 7.
- For paginated responses, document the envelope shape once and link the rest of the route map to it.

---

## Section 6 — Common Envelopes

If the API uses a consistent response envelope, document it once.

```markdown
\`\`\`json
{
  "data": [],
  "meta": { "total": 0, "page": 1, "pageSize": 20 }
}
\`\`\`
```

Cover: pagination shape, error envelope, batch-response shape if present.

---

## Section 7 — Error Handling

```markdown
| HTTP Status | Meaning | Client Behavior |
|---|---|---|
| 401 | Token expired or missing | Refresh token, retry once |
| 403 | Role lacks permission | Show forbidden UI |
| 404 | Resource not found | Empty state |
| 422 | Validation failure | Inline field errors |
| 5xx | Server fault | Toast + retry option |
```

Rules:

- Anchor to the actual interceptor / error handler file.
- Document any retry-with-refresh-token logic.
- Document any error envelope shape.
- Note where API errors get normalized for the UI.

---

## Section 8 — OpenAPI / Swagger (if present)

```markdown
| Resource | Path |
|---|---|
| Spec file | `<path>` |
| UI route (dev) | `<url>` |
| Generated client | `<path>` |
```

If the repo generates clients from a spec, document the regen command and which files are generated (never edit by hand).

---

## Section 9 — Rate Limits / Quotas (if applicable)

Document quota source, default limits, and behavior when exceeded. Skip when not enforced.

---

## Section 10 — Versioning (if applicable)

Document URL versioning (`/v1/`, `/v2/`), header versioning, or deprecation policy.

---

## Section 11 — Related Docs

```markdown
- [Architecture and Walkthrough](./architecture-and-walkthrough.md)
- [Core Concepts](./core-concepts/overview.md)
- [Testing](./testing.md)
- [Code Format, Patterns & Style](./code-format-patterns-style.md)
```

---

## Writing Rules

- Every endpoint cited in this doc must exist in the repo.
- Every type/DTO cited must resolve to a real file path.
- Never document secret values, real tokens, or production hostnames unless they are already public.
- Prefer tables for endpoint maps; prefer JSON blocks for shapes.
- For large surfaces, split per resource: `docs/api/orders.md`, `docs/api/accounts.md`, with `docs/api/README.md` as the index.

---

## Verification

1. Every row in the Route Map maps to a file in the repo.
2. Every request/response shape was pulled from a DTO/schema source, not hand-typed.
3. Authentication section matches the actual interceptor/middleware behavior.
4. Error table reflects the real handler logic.
5. No secret values appear.
6. Links in Related Docs resolve.
7. If OpenAPI/Swagger is present, the regen path is documented.
