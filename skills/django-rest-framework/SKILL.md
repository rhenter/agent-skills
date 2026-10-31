---
name: django-rest-framework
description: Use for Django REST Framework serializers, ViewSets, APIViews, permissions, authentication, pagination, filtering, validation, API architecture, and code organization.
---

# Django Rest Framework

## General Guidelines

- Use serializers for validation, serialization, and representation.
- Follow existing ViewSet, APIView, and generic-view conventions.
- Make authentication, permissions, pagination, and filtering explicit.
- Check queryset efficiency and authorization boundaries.
- Follow DRY, KISS, Clean Code, and Separation of Concerns.
- Prefer existing implementations over unnecessary abstractions.

## Serializer Organization

- Never define serializers inside `models.py`, `views.py`, or `viewsets.py`.
- Always define serializers in a dedicated `serializers.py` file or `serializers/` package.
- For small apps, prefer `serializers.py`.
- For complex apps, use a `serializers/` package organized by resource or responsibility.
- Before creating a serializer, check whether an appropriate implementation already exists.
- Place genuinely reusable serializers in `apps.core.serializers` when shared across multiple apps.
- Import serializers explicitly wherever needed.

## Validation

- Keep field-specific validation inside `validate_<field>()`.
- Keep cross-field validation inside `validate()`.
- Avoid duplicating validation logic across serializers.
- Extract reusable validation helpers into the app's `utils.py`.
- Place helpers shared across multiple apps in `apps.core.utils`.
- Keep validation errors consistent with DRF conventions.

## Business Logic

- Keep domain and business logic out of serializers.
- Delegate complex operations to an existing service layer or an appropriate dedicated module.
- Do not create a service layer unnecessarily for simple operations.
- Keep serializers focused on input validation, data transformation, and representation.

## Serializer Methods

- Use standard DRF methods when appropriate:
  - `validate()`
  - `validate_<field>()`
  - `create()`
  - `update()`
  - `to_representation()`
  - `get_<field>()` for `SerializerMethodField`.
- Avoid overriding DRF methods without a clear reason.
- Keep overridden methods small and focused.

## Views and ViewSets

- Follow existing project conventions before introducing new patterns.
- Prefer DRF generic views and ViewSets when they fit the requirements.
- Keep views focused on HTTP request handling and response orchestration.
- Avoid duplicating validation or business logic across endpoints.
- Use `get_queryset()` when queryset behavior depends on the request or user.
- Apply `select_related()` and `prefetch_related()` where appropriate to avoid N+1 queries.

## Security and API Behavior

- Define authentication and permission requirements explicitly.
- Never rely exclusively on frontend authorization checks.
- Enforce object-level authorization where required.
- Validate and sanitize incoming data through serializers.
- Use appropriate HTTP status codes and consistent error responses.
- Apply pagination and filtering according to existing project conventions.

## Final Checks

Before completing an implementation:

1. Verify that serializers are located in the correct module.
2. Confirm that existing serializers and helpers were reused where possible.
3. Check that business logic is not unnecessarily embedded in serializers.
4. Verify authentication and authorization boundaries.
5. Check database query efficiency.
6. Run relevant tests and project linting tools.
