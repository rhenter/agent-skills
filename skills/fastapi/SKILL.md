---
name: fastapi
description: Use when implementing or reviewing FastAPI services.
---

# FastAPI

## Guidelines

- Use Pydantic models for request and response contracts.
- Use dependency injection for reusable dependencies.
- Keep endpoint handlers small.
- Use async only when the dependency stack and workload benefit from it.
- Define explicit response models and error behavior.

## Before finishing

- Follow the existing project's conventions and `AGENTS.md`.
- Run the relevant formatter, linter, type checker, and tests when available.
- Report assumptions, unresolved risks, and validation you could not perform.
