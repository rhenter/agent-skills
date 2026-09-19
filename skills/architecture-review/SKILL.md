---
name: architecture-review
description: Use when evaluating system design, service boundaries, scalability, or maintainability.
---

# Architecture Review

## Guidelines

- Identify constraints and assumptions before proposing changes.
- Evaluate coupling, cohesion, failure modes, observability, and operational complexity.
- Prefer incremental improvements over rewrites when practical.
- Call out trade-offs explicitly.
- Distinguish current-state observations from recommendations.

## Before finishing

- Follow the existing project's conventions and `AGENTS.md`.
- Run the relevant formatter, linter, type checker, and tests when available.
- Report assumptions, unresolved risks, and validation you could not perform.
