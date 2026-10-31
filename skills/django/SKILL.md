---
name: django
description: Use for Django-specific models, custom fields, ORM, views, middleware, migrations, admin, transactions, utilities, application architecture, and code organization.
---

# Django

## General Guidelines

- Follow DRY, KISS, Clean Code, and Separation of Concerns.
- Follow existing project conventions before introducing new patterns.
- Prefer simple, readable, and maintainable implementations.
- Reuse existing components before creating new ones.
- Avoid unnecessary abstractions and premature optimization.

## Model Organization

- Keep `models.py` focused on model definitions, relationships, constraints, and model-specific behavior.
- Never define custom model field classes directly inside `models.py`.
- Never define standalone utility functions inside `models.py`.
- Keep model methods when they represent behavior belonging to the model.
- Avoid embedding complex business workflows inside models.
- Import custom fields and utilities from their appropriate modules.

## Custom Model Fields

- Before creating a custom model field, check whether `apps.core.fields` already exists.
- If `apps.core.fields` exists, define reusable custom model fields there.
- If it does not exist, create a `fields.py` file within the same Django app as the model.
- Reference custom fields in `models.py` through explicit imports.
- Check for existing custom fields before creating new implementations.
- Keep custom fields reusable and independent of domain-specific business logic whenever possible.

## Utility Functions

- Never define standalone utility functions directly inside `models.py`.
- Place app-specific utility functions in the same app's `utils.py`.
- Place utilities shared across multiple apps in `apps.core.utils`.
- Create the appropriate module if it does not already exist.
- Avoid duplicating utility functions across apps.
- Keep utilities focused, reusable, and easy to test.
- Do not move model-specific behavior into utilities unnecessarily.

## ORM and Query Optimization

- Prefer the Django ORM over raw SQL unless raw SQL provides a concrete benefit.
- Use `select_related()` and `prefetch_related()` when appropriate to prevent N+1 queries.
- Use `only()`, `defer()`, `values()`, and `values_list()` when beneficial.
- Prefer database-side filtering and aggregation over unnecessary Python processing.
- Avoid unnecessary database queries inside loops.
- Use bulk operations when appropriate, considering their limitations.
- Add database indexes based on actual query patterns.
- Prioritize correctness and readability before optimization.

## Views and Business Logic

- Keep views thin and focused on request handling.
- Separate complex business logic into appropriate modules or services.
- Follow existing service-layer conventions when available.
- Do not introduce a service layer for trivial operations.
- Avoid duplicating business logic across views, models, and utilities.

## Transactions

- Use `transaction.atomic()` when multiple database writes must succeed or fail together.
- Keep transactions as short as reasonably possible.
- Avoid unnecessary external API calls inside database transactions.
- Use `transaction.on_commit()` for side effects that must occur after a successful commit.
- Consider concurrency and race conditions when updating shared data.

## Migrations

- Create migrations only when model changes require them.
- Never modify historical migrations without a specific, justified reason.
- Keep schema migrations and data migrations appropriately separated.
- Use `RunPython` with historical models through `apps.get_model()`.
- Review generated migrations before applying them.
- Avoid destructive schema changes without considering existing data.
- Never delete or reset migrations merely to resolve a conflict.

## Django Admin

- Keep admin configuration inside `admin.py` or an existing admin package.
- Use `list_display`, `list_filter`, and `search_fields` appropriately.
- Optimize admin querysets when necessary.
- Avoid complex business logic inside admin actions.
- Respect permissions and authorization requirements.

## Application Structure

- Follow the existing Django app structure.
- Keep app-specific functionality within its corresponding app.
- Place genuinely shared functionality in `apps.core` when appropriate.
- Avoid introducing circular dependencies between apps.
- Do not create new apps or modules without a clear responsibility.
- Prefer explicit imports and predictable module organization.

## Testing

- Add or update tests for changed behavior.
- Prefer existing test conventions and fixtures.
- Test model constraints, validation, and business rules.
- Test transaction behavior when atomicity matters.
- Avoid unnecessary mocking of Django ORM behavior.
- Keep tests isolated and deterministic.

## Final Checks

Before completing an implementation:

1. Verify that custom fields are not defined in `models.py`.
2. Verify that standalone utility functions are not defined in `models.py`.
3. Confirm that reusable components were checked before creating new ones.
4. Check ORM queries for unnecessary database access.
5. Verify transaction boundaries and data integrity.
6. Review migrations for correctness and safety.
7. Ensure the implementation follows existing project conventions.
8. Run relevant tests and project linting tools.
