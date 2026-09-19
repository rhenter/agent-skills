---
name: django
description: Use when implementing, reviewing, or refactoring Django applications.
---

# Django

## Guidelines

- Prefer Django ORM over raw SQL unless raw SQL is justified.
- Prevent N+1 queries; consider select_related() and prefetch_related().
- Keep views thin and separate complex business logic appropriately.
- Use transactions when multiple writes must be atomic.
- Follow Django security practices and existing project architecture.
- Do not create migrations unless model changes require them.

## Before finishing

- Follow the existing project's conventions and `AGENTS.md`.
- Run the relevant formatter, linter, type checker, and tests when available.
- Report assumptions, unresolved risks, and validation you could not perform.
