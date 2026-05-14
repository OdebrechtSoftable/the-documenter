# Commercial Overview — Template

Use this template for `docs/commercial-overview.md`. Audience: commercial team, business stakeholders, executives, and anyone without engineering context. The goal is plain-language understanding, not implementation detail.

Drop sections the repo cannot truthfully fill. Never invent business impact, user groups, or features the product does not have.

---

## Required Header

```markdown
# Commercial Overview

<one-sentence positioning statement: what the product does and for whom>
```

The opening sentence must answer "what is this, and who is it for" in one breath. No jargon, no abbreviations a non-engineer would not recognize.

---

## Section 1 — Who Uses It

A table mapping user groups to their primary need. Pull groups from the auth/roles config (`AGENTS.md`, `authContext`, role enums) or from user-confirmed information.

```markdown
| User Group | Main Need |
|---|---|
| <role/persona> | <one-line need> |
```

Rules:

- Three to six rows max. If you have more, group them.
- "Main Need" is a verb phrase ("See customer activity before outreach"), not a feature list.
- Never describe a user group the product does not actually serve.

---

## Section 2 — Main Functionalities

Bulleted list of what the product does, written in user language. Pull from the route map, top-level page components, and the main features section of `AGENTS.md` / `README.md`.

```markdown
- <feature in user-language>
- <feature in user-language>
```

Rules:

- Five to ten bullets. Cut deeper.
- Each bullet describes a capability the user experiences, not a module or service.
- No tech terms ("React component", "API endpoint", "Redux store").

---

## Section 3 — Business Impact

What changes for the business because this product exists. Three to five bullets.

```markdown
- <observable outcome: time saved, errors avoided, decisions enabled>
```

Rules:

- Outcome-focused, not feature-focused.
- No metrics unless the user confirmed them. "Reduces follow-up time" is fine; "Reduces follow-up time by 40%" requires a source.
- No marketing superlatives ("revolutionary", "best-in-class").

---

## Section 4 — Workflow Fit

One short paragraph (2-4 sentences) describing when in the user's day or process they open the product. Anchor to real moments: "before customer calls", "during weekly review", "when a new order arrives".

---

## Section 5 — Important Limitations

What the product does not do, or where it depends on other systems. Three to six bullets.

```markdown
- <what the product does not own, where data comes from, what it cannot decide>
```

Rules:

- State limitations matter-of-factly. No apology, no spin.
- Include backend / data dependencies the user-facing app does not control.
- Include known UX or workflow gaps that commercial users would otherwise discover the hard way.

---

## Section 6 — Related Docs

Link to deeper reading. Required minimum:

```markdown
- [Core Concepts](./core-concepts/overview.md)
- [Documentation Index](./README.md)
```

Add module docs that match the functionalities listed in Section 2.

---

## Writing Rules

- Plain language. If a sentence cannot be read by someone who has never seen the codebase, rewrite it.
- No code blocks, no architecture diagrams, no class/component names.
- No abbreviations unless the product itself uses them user-facingly.
- No future / aspirational language. Document what exists today.
- Source every business claim to repo evidence or user-confirmed input. Omit claims that have neither.
- Length target: one screen, ~150-300 words.

---

## Verification

Before shipping:

1. Every user group in Section 1 maps to a real role/persona observable in the repo or confirmed by the user.
2. Every functionality in Section 2 maps to a route, page, or major feature in the repo.
3. No technical jargon survived editing.
4. Limitations match real product gaps, not invented humility.
5. Related Docs links resolve.
