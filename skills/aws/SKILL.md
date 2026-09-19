---
name: aws
description: Use for AWS architecture, implementation, and operational tasks.
---

# AWS

## Guidelines

- Prefer least-privilege IAM policies.
- Keep secrets out of source code and images.
- Consider reliability, observability, cost, and failure recovery.
- Prefer managed services when they materially reduce operational burden.
- Avoid destructive infrastructure actions unless explicitly requested.

## Before finishing

- Follow the existing project's conventions and `AGENTS.md`.
- Run the relevant formatter, linter, type checker, and tests when available.
- Report assumptions, unresolved risks, and validation you could not perform.
