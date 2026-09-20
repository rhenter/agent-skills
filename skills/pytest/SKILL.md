---
name: pytest
description: Use when creating or improving Python automated tests.
---

# Pytest

## Guidelines

- Prefer focused tests with clear Arrange/Act/Assert structure.
- Use fixtures for reusable setup, not hidden test behavior.
- Define reusable setup with `pytest.fixture` and prefer built-in pytest fixtures over custom repeated helpers when they fit.
- In Django tests, prefer fixtures such as `admin_client` over manual client/user setup in the style of native `unittest`.
- Mock external boundaries rather than internal implementation details.
- Cover success paths, edge cases, and relevant failures.
- Avoid brittle assertions tied to implementation details.

## Before finishing

- Follow the existing project's conventions and `AGENTS.md`.
- Run the relevant formatter, linter, type checker, and tests when available.
- Report assumptions, unresolved risks, and validation you could not perform.
