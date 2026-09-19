---
name: development-best-practices
description: Use for Python implementation and refactoring tasks. Emphasizes Clean Code, KISS, and the Zen of Python.
---

# Development Best Practices

## Core philosophy

Code should be optimized first for clarity, simplicity, and maintainability.

Follow these principles when making implementation decisions:

### KISS — Keep It Simple

- Prefer the simplest solution that correctly solves the current problem.
- Avoid unnecessary abstractions, layers, patterns, and indirection.
- Do not introduce complexity for hypothetical future requirements.
- Prefer straightforward code over clever code.
- If two solutions are equally correct, prefer the one that is easier to understand and maintain.

### Clean Code

- Use meaningful and intention-revealing names.
- Keep functions and classes focused on a clear responsibility.
- Keep functions reasonably small, but do not split code mechanically just to reduce line count.
- Reduce duplication when doing so improves clarity.
- Avoid hidden side effects.
- Make dependencies and behavior explicit.
- Comments should explain *why* when the code cannot make the reason obvious; avoid comments that merely repeat the code.
- Refactor toward readability rather than abstraction for abstraction's sake.
- Optimize for the next developer reading the code.

### Zen of Python

Use the Zen of Python as a decision-making guide, especially:

- Beautiful is better than ugly.
- Explicit is better than implicit.
- Simple is better than complex.
- Complex is better than complicated.
- Flat is better than nested.
- Sparse is better than dense.
- Readability counts.
- Special cases aren't special enough to break the rules.
- Practicality beats purity.
- Errors should never pass silently unless explicitly silenced.
- In the face of ambiguity, refuse the temptation to guess.
- There should preferably be one obvious way to do it.
- If the implementation is hard to explain, it is probably not a good implementation.
- If the implementation is easy to explain, it may be a good implementation.

## Python guidelines

- Prefer simple, readable, idiomatic Python.
- Use type hints for public APIs and non-trivial functions.
- Follow PEP 8 and the project's existing conventions.
- Avoid mutable default arguments.
- Prefer `pathlib` for filesystem operations when appropriate.
- Prefer standard-library functionality when it solves the problem cleanly.
- Use Python language features when they improve readability, not merely because they are clever or concise.
- Avoid premature optimization.
- Avoid premature generalization.
- Preserve backward compatibility unless the task explicitly permits breaking changes.

## Design decisions

Before adding a new abstraction, helper, service, base class, mixin, design pattern, or dependency, ask:

1. Does it solve a concrete problem that exists now?
2. Does it make the code easier to understand?
3. Is there a simpler solution?
4. Will another developer understand why this exists without extensive explanation?

If the simpler implementation is sufficient, prefer it.

## Before finishing

- Re-read the implementation from the perspective of another developer.
- Remove unnecessary complexity.
- Remove dead code and redundant abstractions introduced by the change.
- Check naming and readability.
- Follow the existing project's conventions and `AGENTS.md`.
- Run the relevant formatter, linter, type checker, and tests when available.
- Report assumptions, unresolved risks, and validation you could not perform.
