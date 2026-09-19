---
name: django-rest-framework
description: Use for APIs built with Django REST Framework.
---

# Django REST Framework

## Guidelines

- Use serializers for validation and representation.
- Choose ViewSets, APIViews, or generic views based on existing project conventions.
- Apply authentication, permissions, pagination, and filtering explicitly.
- Avoid business logic inside serializers when it belongs in the domain/service layer.
- Check queryset efficiency and authorization boundaries.

## Before finishing

- Follow the existing project's conventions and `AGENTS.md`.
- Run the relevant formatter, linter, type checker, and tests when available.
- Report assumptions, unresolved risks, and validation you could not perform.
