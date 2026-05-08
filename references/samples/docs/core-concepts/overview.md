# Core Concepts

This folder explains product concepts needed before reading module docs.

## Concept Model

```text
account -> order -> status -> follow-up
```

## Accounts

An account represents a customer or business entity managed by the commercial team.

## Orders

An order records requested products, current status, and relevant customer context.

## Status

Status describes where an account or order sits in the current workflow. Status values come from the backend API.

## Follow-Up

A follow-up is a commercial action suggested by recent account or order activity.

## Limitations

- The app displays operational data; it does not define backend status rules.
- Status and account ownership rules must match API behavior.

## Related Pages

- [Glossary](./glossary.md)
- [Features](./features.md)
- [Use Cases](./use-cases.md)
