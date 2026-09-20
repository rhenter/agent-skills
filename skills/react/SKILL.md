---
name: react
description: Use when implementing, reviewing, or refactoring React applications, components, hooks, routing, forms, frontend state flows, rendering behavior, accessibility, and React tests.
---

# React

## Guidelines

- Follow the existing React framework and conventions, such as Next.js, Remix, Vite, CRA, or a custom setup.
- Prefer small components with clear props and responsibilities.
- Keep rendering predictable; avoid deriving persistent state from props when a computed value is enough.
- Use hooks according to React rules and keep dependency arrays correct.
- Keep state as local as possible, then lift or centralize it only when the workflow requires shared coordination.
- Avoid unnecessary effects; use effects for synchronization with external systems, not ordinary data derivation.
- Preserve accessibility with semantic elements, labels, keyboard behavior, focus management, and ARIA only when needed.
- Keep forms explicit about validation, submission state, errors, and disabled/loading behavior.
- Use stable keys for lists and avoid indexes when item identity can change.
- Avoid unnecessary memoization; add `memo`, `useMemo`, or `useCallback` only when it solves a measured or obvious rendering problem.
- Respect server/client boundaries in frameworks that support React Server Components.
- Keep data fetching, caching, mutations, and optimistic updates consistent with the project's existing libraries.

## Styling and UX

- Reuse the project's existing design system, component library, icons, and styling approach.
- Build complete UI states: loading, empty, error, success, disabled, and optimistic states when relevant.
- Keep text, controls, and layout responsive without overlap or layout shift.
- Prefer accessible buttons, links, inputs, menus, tabs, dialogs, and form controls over custom interactions.

## Testing

- Prefer behavior-oriented tests with Testing Library or the project's existing UI test approach.
- Test user interactions, visible outcomes, async states, and accessibility-sensitive flows.
- Mock network or external boundaries, not component internals.
- Add browser or visual verification for substantial layout, responsive, or interaction changes when available.

## Before finishing

- Follow the existing project's conventions and `AGENTS.md`.
- Run the relevant formatter, linter, type checker, tests, and browser checks when available.
- Report assumptions, unresolved risks, and validation you could not perform.
