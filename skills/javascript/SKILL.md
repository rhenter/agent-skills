---
name: javascript
description: Use when implementing, reviewing, or refactoring JavaScript or TypeScript code, including Node.js services, browser code, package scripts, build tooling, async flows, modules, and dependency usage.
---

# JavaScript

## Guidelines

- Prefer clear, modern JavaScript or TypeScript over clever or overly compact code.
- Preserve the project's existing module system, runtime target, formatter, linter, and package manager.
- Use TypeScript types for public APIs, non-trivial data shapes, and cross-module contracts when TypeScript is available.
- Handle asynchronous behavior explicitly with `async`/`await`, `Promise` composition, cancellation, and error paths where relevant.
- Avoid hidden global state, implicit mutations, and broad side effects.
- Validate and normalize untrusted inputs at boundaries.
- Prefer standard platform APIs and existing project dependencies before adding new packages.
- Keep dependency changes narrow and justify new runtime dependencies.
- Respect ESM/CommonJS compatibility and avoid mixing patterns unless the project already does.
- Keep browser, server, test, and build-time code concerns separated.
- For frontend UI code, use a framework-specific skill such as `react` when applicable.

## Testing and Tooling

- Use the project's existing test runner, type checker, linter, and formatter.
- Add or update tests for changed behavior, especially async logic, edge cases, and error handling.
- Prefer integration-level tests for module boundaries and focused unit tests for pure logic.
- Keep mocks at external boundaries instead of mocking internal implementation details.

## Before finishing

- Follow the existing project's conventions and `AGENTS.md`.
- Run the relevant formatter, linter, type checker, and tests when available.
- Report assumptions, unresolved risks, and validation you could not perform.
