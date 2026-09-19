---
name: postgres-performance
description: Use when investigating PostgreSQL query or data-access performance.
---

# PostgreSQL Performance

## Guidelines

- Measure before optimizing.
- Check query plans and index usage when relevant.
- Look for N+1 access patterns and unnecessary round trips.
- Consider cardinality, selectivity, locking, transaction scope, and data volume.
- Do not add indexes blindly; explain write/storage trade-offs.

## Before finishing

- Follow the existing project's conventions and `AGENTS.md`.
- Run the relevant formatter, linter, type checker, and tests when available.
- Report assumptions, unresolved risks, and validation you could not perform.
