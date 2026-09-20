---
name: django
description: Use for Django-specific model, ORM, view, middleware, migration, admin, transaction, or application-structure work.
---

# Django

- Prefer the ORM over raw SQL unless raw SQL has a concrete benefit.
- Prevent N+1 queries with `select_related()` / `prefetch_related()` when appropriate.
- Keep views thin and business logic appropriately separated.
- Use transactions when multiple writes must be atomic.
- Create migrations only when model changes require them.
