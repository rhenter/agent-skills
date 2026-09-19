---
name: security-review
description: Use when reviewing application or infrastructure changes for security risks.
---

# Security Review

## Guidelines

- Never hardcode credentials, tokens, passwords, or private keys.
- Use least-privilege access.
- Validate and sanitize untrusted input.
- Review authentication and authorization separately.
- Check secret management, logging exposure, injection risks, and dependency risks.
- Do not weaken security controls merely to make a test pass.

## Before finishing

- Follow the existing project's conventions and `AGENTS.md`.
- Run the relevant formatter, linter, type checker, and tests when available.
- Report assumptions, unresolved risks, and validation you could not perform.
