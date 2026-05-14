# Core Concepts — Template

Use this template for the `docs/core-concepts/` folder. Audience: new engineers and agents who need product-domain grounding before reading module docs.

This folder is required for any repo with non-trivial domain concepts. Create the four canonical files unless the repo already uses an equivalent split (e.g., a single `domain.md`).

```
docs/core-concepts/
├── overview.md
├── glossary.md
├── features.md
└── use-cases.md
```

---

## `overview.md`

The map of the domain. Read first; everything else assumes it.

### Required structure

```markdown
# Core Concepts

This folder explains product concepts needed before reading module docs.

## Concept Model

<one ASCII or Mermaid diagram showing the top-level domain relationships>

## <Concept 1>

<2-4 sentences. What the concept is. Where it lives in the product. Who interacts with it.>

## <Concept 2>

...

## Limitations

- <what the product does not enforce>
- <which rules live in the backend / external system, not here>

## Related Pages

- [Glossary](./glossary.md)
- [Features](./features.md)
- [Use Cases](./use-cases.md)
```

### Diagram requirement

Use a Mermaid `graph` diagram when the domain has more than three concepts with relationships. Fall back to ASCII for simple linear flows.

```markdown
\`\`\`mermaid
graph LR
  Account --> Order
  Order --> Status
  Status --> FollowUp
\`\`\`
```

### Rules

- One H2 per top-level concept. Three to seven concepts total. If you have more, the domain is not yet bounded — split into multiple core-concept docs or push detail into module docs.
- Define concept by what it represents in the product, not by its database table or class name.
- Limitations section calls out where rules live elsewhere (backend, external API, manual process).

---

## `glossary.md`

Single alphabetical table of every domain term the product uses. New engineers consult this when a meeting word lands unfamiliar.

```markdown
# Glossary

| Term | Definition | Source |
|---|---|---|
| Account | <one-sentence definition> | <code path or business owner> |
| Follow-up | <one-sentence definition> | <code path or business owner> |
```

Rules:

- Alphabetical. Strict.
- Definition fits one sentence. If it needs two, push the rest to `overview.md` or a module doc.
- Source column points to the authoritative location: a TypeScript type, an API response field, a backend enum, or a named business owner.
- Include only terms the codebase or product actually uses. No textbook definitions.

---

## `features.md`

The full list of user-visible features, organized by area. Bridges `commercial-overview.md` (user-language) and module docs (engineering-language).

```markdown
# Features

## <Area 1>

### <Feature name>

- **What it does:** <one sentence in user-language>
- **Where it lives:** <route or page path>
- **Owned by:** <module doc link>
- **Status:** stable | beta | deprecated

### <Feature name>

...

## <Area 2>

...
```

Rules:

- Group features under product areas (Orders, Reporting, Admin), not under technical layers (Components, Services).
- Every feature must link to its module doc.
- Mark deprecated features explicitly; do not delete them while still shipped.
- Status field is enumerated: stable / beta / deprecated / planned. Drop "planned" entries that have no in-repo evidence.

---

## `use-cases.md`

End-to-end user journeys. Each one anchored to a real persona, a real entry point, and a real outcome.

```markdown
# Use Cases

## <Use case name>

**Persona:** <user group from commercial-overview.md>
**Entry point:** <how they arrive: route, notification, external link>
**Goal:** <what they want to accomplish>

### Flow

1. <step in user-language>
2. <step in user-language>
3. <step in user-language>

### Related Modules

- [Module Doc](../modules/<module>.md)

### Limitations

- <what does not work in this flow today>
```

Rules:

- Three to eight use cases. If you have more, the product probably needs an `overview.md` rethink.
- Steps are written from the user's perspective. No "the system fetches X" — instead, "the user sees X".
- Every use case has a Persona that matches a row in `commercial-overview.md`'s user-group table.
- Limitations are required when the flow has gaps. Honest > flattering.

---

## Cross-File Rules

- Personas in `use-cases.md` must match user groups in `commercial-overview.md`.
- Terms in `overview.md` headings must each appear in `glossary.md` with a matching definition.
- Features in `features.md` must link to module docs that exist.
- No file in `core-concepts/` should explain implementation details. Push those to module docs.

---

## Verification

1. `overview.md` has a domain diagram (Mermaid or ASCII) and three-to-seven top-level concepts.
2. Every glossary term has a definition and a source.
3. Every feature in `features.md` has a route and a module-doc link.
4. Every use case has a persona, entry point, goal, numbered flow, and module-doc links.
5. No file mentions framework names (React, .NET) except as needed to identify a real path.
6. Cross-file references resolve.
