# Module — Template

Use this template for any file under `docs/modules/`. One file per module/feature. Audience: engineers and agents about to work in that module.

A module doc is operational: someone reading it should be able to locate the code, understand the user flow, and make a safe edit. Skip sections that the module does not exercise.

---

## Required Header

```markdown
# <Module Name>

<one-sentence statement: what this module does in the product>
```

Module name matches a row in `docs/core-concepts/features.md`. The opening sentence should be in user-language, not implementation-language.

---

## Section 1 — Purpose

One short paragraph (2-4 sentences). What user need does this module address? Who interacts with it?

Cite the persona from `docs/commercial-overview.md` if applicable.

---

## Section 2 — User Flow

A Mermaid diagram of the canonical happy path through the module.

```markdown
\`\`\`mermaid
graph LR
  EntryPoint[Orders page] --> Filters
  Filters --> List[Order list]
  List --> Detail[Order detail]
  Detail --> Action[Follow-up action]
\`\`\`
```

For simple linear flows, ASCII is acceptable:

```text
orders page -> filters -> order list -> order detail -> follow-up action
```

Below the diagram, optionally add 3-6 bullets describing each step in user-language.

---

## Section 3 — Key Paths

The canonical table for navigating the module's code.

```markdown
| Path | Purpose |
|---|---|
| `src/pages/<feature>.tsx` | Route entry |
| `src/components/pages/<Feature>/` | Page-level components |
| `src/components/pages/<Feature>/hooks/` | Page-scoped hooks |
| `src/components/pages/<Feature>/sections/` | Major JSX blocks |
| `src/services/api/<feature>/` | API client modules |
| `src/dtos/<feature>/` | Request/response types |
| `src/contexts/<feature>/` | Feature context, if any |
| `src/hooks/<feature>/` | Cross-page hooks, if any |
```

Rules:

- Every row must point to a path that exists.
- Order: entry point first, then components, hooks, services, types, contexts.
- For backend modules, swap to controllers/services/repositories/migrations.

---

## Section 4 — Behavior

What the module does in observable terms. Bullet list, no narrative.

```markdown
- <what loads on mount>
- <what filters affect>
- <what triggers writes>
- <what the empty state looks like>
- <what the error state looks like>
- <what the loading state looks like>
```

Rules:

- One bullet per observable behavior. If you need a paragraph, push the detail into a sub-section.
- Cover the four UI states explicitly: loading, empty, error, populated.
- For backend modules, cover: input validation, side effects, persistence boundaries, external calls, observable outputs.

---

## Section 5 — Data Flow

A Mermaid or ASCII diagram showing where data enters, where it transforms, and where it exits.

```markdown
\`\`\`mermaid
graph LR
  API[GET /orders] --> Hook[useOrders]
  Hook --> Section[OrdersSection]
  Section --> Detail[OrderDetails]
  Detail --> Mutation[PUT /orders/:id]
  Mutation --> Refresh[refreshOrders]
\`\`\`
```

Cover: which API endpoints the module calls, which hooks consume them, where mutations happen, how refresh propagates.

For modules with no API surface (pure UI/utility), skip this section.

---

## Section 6 — Domain Rules

Business rules the module enforces or assumes. Use a numbered list when the rules interact.

```markdown
1. <rule>
2. <rule>
3. <rule>
```

Rules:

- Pull from actual code (validators, guards, mappers, role checks), not from intuition.
- Cite the file path for each rule when non-trivial.
- If a rule lives in the backend, say so and link to the backend doc.

---

## Section 7 — Known Issues

Bugs, gaps, or rough edges the next engineer should know about.

```markdown
- <issue> — <workaround if any>
- <issue> — <ticket link if any>
```

Rules:

- Include user-confirmed known issues even when not yet ticketed.
- Mark TODO/FIXME comments in the source if they're load-bearing.
- Omit if there genuinely are none — do not fabricate.

---

## Section 8 — Before Editing

Operational checklist specific to this module. Short.

```markdown
- Confirm <X> before touching <Y>.
- Run <command> to verify <Z>.
- Coordinate with <module / team> when changing <shared concept>.
```

Rules:

- Module-specific gotchas only. Generic "run lint before commit" belongs in `AGENTS.md`.
- If editing this module commonly breaks another module, name the other module and the failure mode.

---

## Section 9 — Related Docs

```markdown
- [Core Concepts](../core-concepts/overview.md)
- [API](../api.md)
- [Architecture and Walkthrough](../architecture-and-walkthrough.md)
- [Code Format, Patterns & Style](../code-format-patterns-style.md)
- [<sibling module>](./<sibling>.md)
```

---

## Writing Rules

- Path-first. Tables and diagrams beat prose.
- Every cited path must exist. Stale paths are bugs.
- Module name in title matches the folder name in code (PascalCase) and the feature name in `features.md` (user-language) — note both if they differ.
- Length target: one screen plus diagrams (~300-500 words).
- Do not duplicate `AGENTS.md` rules or `code-format-patterns-style.md` conventions. Link to them.
- Update the module doc when its code changes. Drift is a doc bug.

---

## Verification

1. Every path in Section 3 exists.
2. User flow diagram matches the actual route + state transitions.
3. Data flow diagram matches the actual hook/API wiring.
4. All four UI states are covered in Section 4 (loading, empty, error, populated) — or it's explicitly noted which the module does not have.
5. Known issues were asked about during the documentation pass.
6. Related Docs links resolve.
7. Module appears in `docs/core-concepts/features.md` with a matching link.
