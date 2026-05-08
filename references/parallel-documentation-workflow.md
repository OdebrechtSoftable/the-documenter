# Parallel Documentation Workflow

Use this workflow when The Documenter creates or refreshes a large doc set.

Parallelization must improve throughput without weakening evidence quality. Do not parallelize from raw repo context alone.

## Core Principle

Create a source documentation layer first. Then use faster parallel agents for docs that summarize, route, or operationalize that source layer.

```text
repo evidence -> module docs -> core concepts -> shared facts -> parallel derived docs -> serial merge/verify
```

## When To Use

Use this workflow for:

- large repos
- full-stack repos
- many modules/features
- full doc-pack creation
- stale docs where multiple files need refresh

Do not use it for:

- one narrow doc edit
- small repos where one pass is faster
- unclear facts that require immediate user answers
- docs that need one tightly held product narrative

## Serial Phase 1: Evidence Scan

The orchestrator owns initial evidence gathering.

Inspect:

- target repo `AGENTS.md`
- current `README.md`, `docs/README.md`, `CLAUDE.md`
- manifests, lockfiles, `.sln`, `.csproj`, runtime entry points
- config examples and safe env var names
- CI/deploy files
- module folders and existing module docs
- tests, scripts, and supported commands

Produce working notes with:

| Fact Type | Required Content |
|---|---|
| Repo identity | project name, purpose, stack |
| Commands | exact repo-supported commands |
| Paths | real paths only |
| Modules | module list in build/runtime order |
| Config | safe names only, no values |
| Deploy | CI/CD or platform evidence |
| Unknowns | facts to ask user |

Do not commit this manifest unless the user asks for an artifact. It is coordination context for documentation writers.

## Serial Phase 2: Module Docs

Create or refresh module/feature docs first, ordered by how the product or runtime is built.

Module docs are the factual base for later summaries.

Each module doc should include:

- purpose
- user or runtime flow
- key paths
- main behaviors
- integrations
- data/API touchpoints
- known limits or gotchas
- related docs

Quality gate before moving on:

1. Every cited module path exists.
2. Module behavior is backed by code or existing docs.
3. No command/env/deploy facts are inferred from prose only.
4. Missing facts are omitted or listed as questions.

## Serial Phase 3: Core Concepts

Create `docs/core-concepts/*` after module docs.

Core concepts must normalize language across modules:

- domain terms
- product concepts
- feature benefits
- use cases
- limitations
- illustrations or basic snippets when useful

Avoid making core concepts mirror implementation names. Concepts should explain the product/domain first, then link to module docs.

Quality gate before parallel work:

1. Terms match module docs.
2. Concepts are understandable without reading code.
3. Limitations are plain and factual.
4. Commercial or user-facing terms are user-confirmed when repo evidence is weak.

## Serial Phase 4: Shared Facts Manifest

Before spawning parallel writers, the orchestrator prepares a concise shared facts packet.

Include:

```text
Project:
Stack:
Package/runtime manager:
Commands:
Important paths:
Module docs:
Core concept docs:
Config names:
Deployment evidence:
Testing evidence:
Known issues:
License/versioning:
Forbidden claims:
```

This packet is the common context for every derived-doc writer.

## Parallel Phase: Derived Docs

Use faster/lighter agents only for bounded output after module docs and core concepts exist.

Assign disjoint ownership.

| Agent | Owns | Reads | Must Return |
|---|---|---|---|
| README writer | `README.md` | shared facts, core concepts, docs list | concise human entry point |
| Docs hub writer | `docs/README.md` | shared facts, all doc paths | navigation map and reading path |
| Commercial writer | `docs/commercial-overview.md` | core concepts, module docs, user-confirmed business facts | nontechnical overview |
| Ops writer | `docs/testing.md`, `docs/deployment.md` | shared facts plus repo command/deploy evidence | supported checks and deployment runbook |
| API/design writer | API docs, `docs/DESIGN.md`, architecture refinements | module docs plus stack entry point refs | focused technical docs |
| Agent-docs writer | `AGENTS.md`, `CLAUDE.md` | shared facts plus repo operational evidence | operational guide and pointer-only Claude |

Parallel agents must not:

- invent commands, paths, env vars, deploy steps, owners, license, or versioning
- document secret values
- write outside assigned files
- treat module/core docs as proof for commands, env vars, or deployment
- duplicate full deployment/API/module details in root `README.md`
- duplicate `AGENTS.md` in `CLAUDE.md`

## Agent Context Packet

Each parallel agent gets:

1. assigned file ownership
2. shared facts manifest
3. paths to module docs and core concepts
4. relevant template/reference file
5. hard prohibitions
6. expected return format

Example:

```text
Own only README.md.
Read shared facts, docs/README.md target list, docs/core-concepts/*, module docs.
Write concise human README.
Do not include deployment runbook, full API map, secrets, unsupported commands, or AGENTS rules.
Return changed file path and any omitted facts.
```

## Serial Merge

The orchestrator reviews every parallel output.

Merge checklist:

1. Root README is concise and links to `docs/README.md`.
2. `docs/README.md` owns detailed navigation.
3. Deployment details live in `docs/deployment.md`.
4. `CLAUDE.md` only points to `AGENTS.md`.
5. Shared facts match across README, docs hub, AGENTS, testing, deployment, and API docs.
6. Every cited path exists.
7. Every finite documented command is run.
8. Long-running commands are smoke-started when safe.
9. Env/config docs list names only, never values.
10. Missing facts are omitted.
11. No parallel writer introduced unsupported claims.

## Performance Tradeoff

This workflow intentionally delays parallelism until the source layer is strong.

Cost:

- slower start
- heavier orchestrator review
- module-doc mistakes can propagate

Benefit:

- lower context loss for parallel agents
- better terminology consistency
- fewer invented facts
- faster completion for large doc sets after source docs exist

## Scale Rules

| Repo Size | Parallelism |
|---|---|
| Small | Keep serial |
| Medium | Parallelize 1-2 derived-doc writers after module/core docs |
| Large | Parallelize 3-5 derived-doc writers after module/core docs |
| Full-stack | Split by frontend/backend only after shared concepts and module docs exist |

The orchestrator remains responsible for final correctness.
