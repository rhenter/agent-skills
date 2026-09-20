# Agent Skills

Reusable agent skills for Codex, Cursor, and other tools compatible with
`SKILL.md`.

These skills are intentionally tool-agnostic and project-agnostic. Keep reusable
engineering guidance here. Put project-specific architecture, commands, business
rules, credentials, and constraints in each project's `AGENTS.md`.

## Installation

Clone this repository:

```bash
git clone git@github.com:rhenter/agent-skills.git ~/agent-skills
```

### Codex

Expose the skills through Codex's global skills directory:

```bash
mkdir -p ~/.codex
ln -s ~/agent-skills/skills ~/.codex/skills
```

If `~/.codex/skills` already exists, back it up or remove it before creating the
symlink.

### Other Agents

For tools that read from `~/.agents/skills`, expose the same directory there:

```bash
mkdir -p ~/.agents
ln -s ~/agent-skills/skills ~/.agents/skills
```

If `~/.agents/skills` already exists, back it up or remove it before creating the symlink.

## Available Skills

| Skill | Use when... |
| --- | --- |
| `architecture-review` | Evaluating system design, service boundaries, scalability, or maintainability. |
| `aws` | Working on AWS architecture, implementation, or operations. |
| `code-review` | Reviewing code changes or pull/merge requests. |
| `django` | Implementing, reviewing, or refactoring Django applications. |
| `django-rest-framework` | Working on APIs built with Django REST Framework. |
| `fastapi` | Implementing or reviewing FastAPI services. |
| `javascript` | Implementing, reviewing, or refactoring JavaScript or TypeScript code. |
| `kubernetes` | Working on Kubernetes deployment, troubleshooting, or architecture tasks. |
| `postgres-performance` | Investigating PostgreSQL query or data-access performance. |
| `pytest` | Creating or improving Python automated tests. |
| `python-best-practices` | Implementing or refactoring Python code with clean, simple patterns. |
| `react` | Implementing, reviewing, or refactoring React applications and components. |
| `security-review` | Reviewing application or infrastructure changes for security risks. |

## Structure

Each skill lives in `skills/<skill-name>/SKILL.md`.

```text
skills/<skill-name>/
├── SKILL.md
├── references/   # optional detailed docs, loaded only when needed
├── scripts/      # optional repeatable commands or deterministic helpers
├── assets/       # optional templates, images, or other reusable files
└── agents/       # optional UI metadata for agent surfaces
```

Current skills only need `SKILL.md`. Add optional directories only when they
directly support repeated work.

## Authoring Guidelines

- Use lowercase kebab-case for skill folder names.
- Match the folder name to the `name` field in `SKILL.md`.
- Keep `SKILL.md` concise, procedural, and broadly reusable.
- Put detailed reference material in `references/` instead of bloating
  `SKILL.md`.
- Put fragile or repeated commands in `scripts/`.
- Put reusable templates, examples, or static inputs in `assets/`.
- Avoid README files inside individual skill folders.
- Keep project-specific details in each project's `AGENTS.md`, not here.

## Skill Template

```md
---
name: example-skill
description: Use when ...
---

# Example Skill

## Guidelines

- Prefer ...
- Avoid ...

## Before finishing

- Run relevant validation when available.
- Report assumptions, risks, and validation that could not be performed.
```
