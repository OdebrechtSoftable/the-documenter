# Code Format, Patterns & Style — Template

Use this template for `docs/code-format-patterns-style.md` in any repo with non-trivial source code. Evidence-first: every rule must cite a concrete repo path or named export. Drop sections that the repo does not actually use.

Pair with `AGENTS.md` — Formatting Rules, Code Style Rules, and File Placement sections in `AGENTS.md` must point here. This doc is the source of truth for code shape.

---

## Document Header (always include)

```markdown
# Code Format, Patterns & Style — <repo-name>

Evidence-based style guide for `<repo-name>` (<stack summary: framework, language, styling system>). Pair with [`CLAUDE.md`](../CLAUDE.md) and [`AGENTS.md`](../AGENTS.md). Every rule below maps to an observable pattern in `<source-root>/`.
```

---

## Section 1 — Tooling Config

Document every tool that shapes code on disk. Skip tools the repo does not use.

For each tool, show:
- The config file path (e.g., `prettier.config.js`, `.eslintrc`, `tsconfig.json`, `.editorconfig`, `pyproject.toml`, `commitlint.config.js`).
- The relevant rules verbatim (small block).
- A plain-language summary of what the rules mean for someone writing code (e.g., "No semicolons", "Single quotes", "No trailing commas").

For TypeScript / language configs, include:
- Strictness flag and its consequences.
- Target / module / JSX setting if non-default.
- **Path aliases as a table** — every alias the repo defines, with its resolved path. Add a one-line rule: "Always use aliases; never `../../`".

For commits, name the convention (Conventional Commits, gitmoji, etc.) and the enforcement hook (husky `commit-msg`, GitHub Action).

For package manager, name it and how it is pinned (`packageManager` field, lockfile presence).

---

## Section 2 — Naming Conventions

A single table covering everything that has a name in the repo. Columns: **Kind**, **Convention**, **Example from repo**.

Kinds to cover when applicable:

- Component file
- Hook file
- HOC
- Feature module folder
- Util file
- Constants
- Type / Interface
- Mapper export
- Styled component
- Transient style prop
- API endpoint folder
- Context provider + hook pair
- Test file
- Story file
- Migration file

Every example must be an actual path or symbol that exists in the repo.

---

## Section 3 — Folder Patterns

Show ASCII trees **plus a Mermaid hierarchy diagram** for the canonical folder shapes the repo uses. The Mermaid diagram is required when the repo has more than one canonical folder shape (component / page / API), so readers can scan the layout visually before diving into trees.

```markdown
\`\`\`mermaid
graph TD
  src --> components
  src --> pages
  src --> services
  src --> hooks
  components --> commons[commons - reusable UI]
  components --> feature[pages - feature modules]
  services --> api[api - per-domain axios + endpoints]
  services --> domains[domains - feature business logic]
\`\`\`
```

Then one ASCII tree per folder kind:

### Common component folder

```
ComponentName/
├── index.tsx
├── styles.ts
├── types.ts                # when non-trivial
├── components/             # sub-components when > 1 internal piece
└── mappers/                # variant → css/color/label
```

### Page / feature folder

```
FeatureName/
├── index.tsx               # composition only — no logic
├── styles.ts
├── hooks/                  # page-scoped
├── sections/               # large JSX blocks split out of index
├── types/
└── utils/                  # pure helpers
```

### API endpoint folder (when repo uses one)

```
services/api/<feature>/
├── api.ts                  # axios instance + interceptors
├── index.ts                # barrel re-export
└── orders.{orderId}.put/   # endpoint folder = URL shape + verb
    ├── index.ts            # the call (named export)
    ├── request.ts          # HttpXxxParams types
    └── response.ts         # HttpResponse type
```

Add one short paragraph after each tree explaining when each pattern applies (simple vs. complex component, page-scoped vs. cross-page hook, etc.).

---

## Section 4 — Component / Module Skeleton

Start with a **Mermaid composition diagram** showing how a typical feature component is composed (page → sections → common components → toolkit primitives → styled components).

```markdown
\`\`\`mermaid
graph TD
  Page[Feature page] --> Section1[FiltersRow]
  Page --> Section2[OrdersSection]
  Section1 --> Common1[SearchInput]
  Section1 --> Common2[Button]
  Section2 --> Common3[Table]
  Common1 --> Styled1[Container + StyledInput]
  Common2 --> Styled2[Container + ButtonContent]
  Common3 --> Toolkit[Typography + Icon]
\`\`\`
```

Then show one canonical example (copy-paste from a real repo file). Then list the rules numbered.

```tsx
// External Libraries
import React, { useState } from 'react'

// Components
import { Foo } from '@components/Foo'

// Hooks
import { useBar } from '@hooks/useBar'

// Utils
import { baz } from '@utils/functions'

// Types
import type { Props } from './types'

// Styles
import { Container } from './styles'

export const MyComponent: React.FC<Props> = props => {
  // States
  // Refs
  // Hooks
  // Constants
  // Effects
  // Functions
  return <Container>...</Container>
}
```

**Rules to document:**

1. Import group order and the label-comment convention.
2. `import type { ... }` for type-only imports.
3. Body section order and the label-comment convention.
4. Function-declaration style (`function` vs. arrow, where each applies).
5. Export style (named vs. default — call out framework exceptions like Next.js page wrappers).
6. Typing convention (`React.FC<Props>`, etc.).

---

## Section 5 — Styling System

Pick the heading that matches the repo's primary system: styled-components / Tailwind / CSS Modules / Emotion / vanilla-extract / Stylesheet (RN) / etc.

Document:

- **File layout** for styles (co-located `styles.ts`, separate `*.module.css`, single-file Tailwind class soup).
- **Style rules** — transient props convention, theme-access pattern, allowed units, layout primitives, conditional CSS helper, hover/disabled idioms, where mappers/variant resolvers live.
- **Theme tokens** — pull the actual token map from the repo into a code block. Cover colors, spacing scale, border-radius, typography, z-index, breakpoints. Add a "Always pull from theme; hardcode only inside the theme file" rule.
- **Global styles** — what `globals.css` / `GlobalStyle` defines (reset, fonts, body defaults, library overrides).
- **Responsive helpers** — facepaint, breakpoint hooks, Tailwind screens. Include the actual breakpoint table.
- **SSR / hydration setup** if applicable (`_document.tsx` `ServerStyleSheet`, Next.js `app` boundaries).

---

## Section 6 — TypeScript Patterns

- Props interface splitting — when to split (style props vs. text props vs. event props) with an example from the repo.
- Extending native HTML props — `Omit<InputHTMLAttributes<HTMLInputElement>, 'onChange'>` pattern.
- Union string literals for variants vs. enums.
- HTTP type naming — `HttpResponse`, `HttpRequestBody`, `HttpXxxParams`. Show where these live.
- DTO placement — `src/dtos/<feature>/` or equivalent.
- `import type` vs. `import` rules (especially under `isolatedModules`).
- When `unknown` / `never` / `Record<string, ...>` are preferred over `any`.

---

## Section 7 — Data Fetching

Start with a **Mermaid sequence diagram** of the canonical request lifecycle (component → hook → client → interceptor → API → response → cache → component).

```markdown
\`\`\`mermaid
sequenceDiagram
  participant Component
  participant Hook as useX (SWR)
  participant Client as axios instance
  participant Interceptor as applyToken
  participant API
  Component->>Hook: render with params
  Hook->>Client: getX(params)
  Client->>Interceptor: attach Bearer token
  Interceptor->>API: request
  API-->>Interceptor: response
  Interceptor-->>Client: response.data
  Client-->>Hook: typed payload
  Hook-->>Component: { data, isLoading, refreshX }
\`\`\`
```

Then show the canonical fetch pattern with a code snippet from the repo. Cover:

- Client library (SWR / React Query / Apollo / fetch + custom hook).
- Cache-key convention (URL string with serialized params, query-key array, etc.).
- Default options (e.g., `revalidateOnFocus: false`).
- Conditional fetch idiom (returning undefined, `enabled: false`, `skip`).
- Stale-data retention pattern (`useRef` for previous data, `keepPreviousData`).
- Mutation/refresh function rename convention (`mutate` → `refreshX`).

### HTTP client

- One axios/fetch instance per domain, or a shared one.
- Path: `services/api/<domain>/api.ts`.
- Request interceptor for auth tokens.
- Response interceptor for 401 retry / refresh.
- Single named-export per endpoint folder; returns `response.data`, never the raw response.

---

## Section 8 — Hooks & Contexts

### Hook structure

Show a canonical hook with the same body-section order as components. Cover:

- Page-scoped hooks vs. cross-page hooks (where each lives).
- Return shape — object only, never tuple. List the convention for what to expose.
- Rename rules (e.g., `mutate` → `refreshOrders`).

### Context pattern

```ts
const XContext = createContext<IXContextData>({} as IXContextData)

const XProvider: React.FC<PropsWithChildren> = ({ children }) => { ... }

function useX(): IXContextData {
  const context = useContext(XContext)
  if (!Object.keys(context)?.length)
    throw new Error('useX must be within an XProvider')
  return context
}

export { XProvider, useX }
```

Cover:

- Default value cast (`{}` as type) plus runtime guard.
- One folder per context (`index.tsx` + `types.ts` + optional `utils/`, `constants.ts`).
- Export pair (`XProvider`, `useX`) at file bottom.

---

## Section 9 — Routing & Pages

- Router in use (Next.js Pages Router, App Router, Vite + react-router, Expo Router). State which patterns are forbidden by repo choice (`getServerSideProps` under static export, App Router conventions in a Pages Router repo, etc.).
- Page wrapper convention (thin file in `src/pages/*` that re-exports the real feature component plus auth/role HOC).
- Protected route pattern (HOC, middleware, layout wrapper).
- Build-time constraints (static export, edge runtime, SSR).
- Dependencies in `package.json` that are present but unused — call out any so contributors don't reach for them.

---

## Section 10 — i18n / Localization (if applicable)

- `useTranslation()` (or equivalent) signature and return shape.
- Where translation JSON lives.
- Country / locale resolution and fallbacks.
- Key-path typing (`NestedKeyOf<typeof brasil>` or library equivalent).
- Behavior on missing key (return key, throw, return placeholder).

---

## Section 11 — Utility Functions

- Purity rule — one function per file, named after main export, no side effects.
- Barrel re-export through `index.ts`.
- Mapper placement (`utils/mappers/`).
- Constants placement (`utils/constants/`).
- Default-value pattern, nullish-safe pattern (`value ?? 0`, optional chaining on outputs), and try/catch fallback style. Show one canonical example.

---

## Section 12 — Error & Auth Patterns

- 401 retry strategy (refresh token, replay with `_retry` flag).
- Failed-refresh fallback (where to redirect, what to stash in storage).
- Auth state shape (`useAuth()` return).
- RBAC: how roles/groups are checked, what bypasses the check (e.g., admin role).
- Impersonation / debug-role mechanics, if present.

---

## Section 13 — Anti-Patterns Table

`| Don't | Do |` table. Aim for 10-15 rows. Each row must reflect an actual mistake observable in the codebase or in PR history.

Common categories to consider:

- Relative imports vs. aliases
- Inline `style={}` vs. styled component
- Hardcoded colors vs. theme token
- Default vs. named exports
- Arrow vs. `function` for component-internal handlers
- Raw `@media` vs. responsive helper
- Trailing comma / semicolon / quote style (mirroring Prettier)
- Forbidden runtime APIs given build/deploy constraints

---

## Section 14 — New-Code Checklist

Short bullet list (8-12 items) a contributor can run through before opening a PR. Pull the highest-leverage rules from earlier sections. Examples:

- [ ] Folder name matches convention.
- [ ] `index.tsx` + `styles.ts` split; types in `types.ts` if non-trivial.
- [ ] Imports grouped with labels, `@alias` paths, type-only imports tagged.
- [ ] Body sections labeled.
- [ ] `function` keyword for component-internal handlers.
- [ ] Styled components use theme tokens; transient props prefixed `$`.
- [ ] Prettier-clean (no semi, single quotes, no trailing commas — whatever the repo enforces).
- [ ] API endpoint folder shape respected (`endpoint.{param}.verb/` + `index.ts` + `request.ts` + `response.ts`).
- [ ] Custom hook returns named object; mutation exposed as `refreshX`.
- [ ] Page route in `src/pages/` is a thin wrapper around feature component + auth HOC.

---

## Writing Rules for This Doc

- Every rule cites a concrete repo file path or named export. No abstract advice.
- Code snippets pulled verbatim from the repo (or stylistically faithful). Mark with the source path when helpful.
- Tables and code blocks first. Prose is trimmed.
- Where the repo violates its own convention, mark the violation in the anti-patterns table — do not rewrite history.
- Do not duplicate `AGENTS.md` operational rules. Link both ways: `AGENTS.md` points here; this doc points to `AGENTS.md` for operational guidance.
- Drop any section the repo does not actually exercise. A backend-only repo skips styling/SSR/responsive helpers; a CLI tool skips routing.

---

## AGENTS.md Pointer (required)

In `AGENTS.md`, the Formatting Rules, Code Style Rules, and File Placement sections must each end with:

```markdown
See [docs/code-format-patterns-style.md](./docs/code-format-patterns-style.md) for the full code format, patterns, and style reference.
```

Keep the in-`AGENTS.md` summary under ~15 lines per section: the 3-5 highest-leverage rules plus the pointer.
