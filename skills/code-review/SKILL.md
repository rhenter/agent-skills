---
name: code-review
description: Use when reviewing code changes or pull/merge requests.
---

# Code Review

## Guidelines

- Prioritize correctness, security, regressions, maintainability, and performance.
- Identify concrete issues with file/location context when available.
- Separate blocking problems from optional improvements.
- Avoid style-only comments when automated tooling can enforce the rule.
- Check tests and missing test coverage for changed behavior.

## Before finishing

- Follow the existing project's conventions and `AGENTS.md`.
- Run the relevant formatter, linter, type checker, and tests when available.
- Report assumptions, unresolved risks, and validation you could not perform.
