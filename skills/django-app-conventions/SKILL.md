---
name: django-app-conventions
description: Implement or review Django and Django REST Framework code using rich models, native serializers, object-oriented workflows, pluggable apps, and conventional package layouts. Use for Django models, serializers, views, domain logic, app architecture, or project-structure work.
---

# Django App Conventions

Apply these conventions together with the repository's local instructions. When local instructions
make a stricter compatible choice, follow them. If existing code violates these conventions, do not
treat it as precedent; improve only the scope touched by the task unless a broader refactor was
requested.

## Native DRF boundaries

- Use `ModelSerializer` for model-backed CRUD and `Serializer` for commands or non-model input.
- Let serializers own parsing, type coercion, field validation, representation, and supported
  create/update behavior.
- Prefer serializer fields, validators, `validate_<field>()`, `validate()`, `create()`, and `update()`
  over custom request-processing functions.
- Views and ViewSets must pass request data through a serializer and return serializer output. Do not
  manually parse payloads or build model representations when a serializer can express the contract.
- Keep each invariant authoritative in one place. Do not repeat the same rule in a view, serializer,
  service, and model.

## Rich models without duplicated logic

- Put entity invariants, calculations, state transitions, and behavior owned by one aggregate on the
  model.
- Put reusable ORM queries and query behavior in custom `QuerySet` and manager classes.
- Prefer intention-revealing domain methods over repeated conditionals and query fragments.
- Keep database constraints near the model and expose model validation when callers need errors
  before persistence.
- Do not make a model coordinate external I/O, long-running tasks, or unrelated aggregates.

## Object-oriented workflows

- Prefer Django and DRF framework classes plus domain objects: ViewSets, serializers, models,
  managers, querysets, policies, adapters, importers, and named use-case classes.
- Use a cohesive application class with explicit dependencies and one clear public operation when a
  workflow spans models, transactions, apps, or external systems.
- Do not create a generic `services.py` containing unrelated module-level public functions.
- Allow module-level functions only when they are small, stateless, private helpers and a class would
  add no responsibility, state, lifecycle, or extension point.
- Do not create classes that merely collect unrelated static methods.

## Pluggable app boundaries

- Give each business capability its own Django app. Do not accumulate unrelated models and endpoints
  in a generic project, backoffice, or core app.
- Each app owns its models, migrations, admin, serializers, views, routes, translations, and tests.
- The project URL configuration only includes app route modules. An app never registers another
  app's endpoints.
- Apps must not import another app's views, serializers, routes, admin, or private implementation.
- Keep cross-app dependencies explicit, minimal, and one-way through stable model references or a
  small public interface.
- Keep shared/core apps small and domain-neutral. Integration adapters belong to dedicated apps and
  must translate external schemas into public domain operations.

## Conventional modules and packages

- Keep Django's conventional `models.py`, `serializers.py`, `views.py`, and `admin.py` while one file
  is sufficient.
- When a responsibility needs a second file, replace the singular module with a package in the same
  change, for example `models/product.py` and `models/barcode.py`.
- Re-export public classes from the package `__init__.py` to preserve Django discovery and stable
  imports.
- Do not scatter files such as `product_model.py`, `product_serializer.py`, or `product_view.py` at
  the app root.
- Organize by responsibility first and domain concept second. Avoid generic helper dumping grounds.

## Language and internationalization

- Keep source code, identifiers, comments, docstrings, internal logs, and test descriptions in
  English.
- Give each app config, model, and model field an English `verbose_name` marked for translation.
  Models also require an internationalized `verbose_name_plural`.
- Internationalize choice labels, help text, validation messages, API errors, accessibility text,
  and every other user-facing string.
- Let request locale negotiation, including `Accept-Language`, select response language. Do not
  force a presentation language inside views, serializers, models, or workflows.

## Completion review

Before finishing, verify and report:

1. HTTP input and output use native serializers.
2. Domain behavior lives on its owning model, manager, or queryset without duplicated rules.
3. Cross-model workflows use a named class rather than loose public functions.
4. The change stays in the correct app and introduces no reverse or circular dependency.
5. A second model, serializer, or view file triggered conversion to a package.
6. Routes remain app-owned and are only included by the project URL configuration.
7. Code is English and all user-facing text and model metadata are translatable.
8. Relevant focused tests, the full suite, lint, Django checks, and migration checks pass.
