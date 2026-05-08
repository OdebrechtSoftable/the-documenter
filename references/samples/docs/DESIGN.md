# Design

## Product Experience

The sample UI is task-focused and optimized for repeated operational work.

## Information Architecture

| Area | User Task |
|---|---|
| Account activity | Review recent customer state |
| Orders | Review order status and follow-up needs |
| Filters | Narrow activity by territory, status, or date |

## Visual System

| Area | Rule / Source |
|---|---|
| Components | Shared components under `src/components/` |
| Styling | Project style system |
| Empty states | Show direct explanation and next action when evidence exists |

## Interaction Patterns

Forms validate before submit. Tables support scanning, filtering, and empty states.

## Accessibility

Interactive controls use visible labels. Error states are shown in text, not color alone.

## Responsive Behavior

Tables collapse into stacked rows on narrow screens.

## User-Facing Language

Use account, order, status, and follow-up consistently with core concepts.

## Known Design Constraints

The sample app uses backend-provided status names; UI copy should not rename workflow states.
