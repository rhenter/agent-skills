---
name: kubernetes
description: Use for Kubernetes deployment, troubleshooting, and architecture tasks.
---

# Kubernetes

## Guidelines

- Define resource requests and limits where appropriate.
- Use readiness and liveness probes intentionally.
- Keep secrets out of manifests committed to source control.
- Consider rollout safety, autoscaling, disruption, and observability.
- Prefer declarative, reproducible configuration.

## Before finishing

- Follow the existing project's conventions and `AGENTS.md`.
- Run the relevant formatter, linter, type checker, and tests when available.
- Report assumptions, unresolved risks, and validation you could not perform.
