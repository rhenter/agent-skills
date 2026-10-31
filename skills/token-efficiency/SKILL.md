---
name: token-efficiency
description: Use at the start of any coding or analysis task to cut token usage without losing quality: minimal scope, surgical file reads, few iterations, and incremental delivery.
---

# Token efficiency

Goal: deliver the requested result while spending as little context as possible. Follow these steps in order.

## 1. Before acting

- Restate the task in one sentence: expected outcome plus the likely files or folders. If a missing detail would change the implementation, ask ONE short question; otherwise assume the project's existing convention and state the assumption.
- If the task is large, split it into small, verifiable deliveries (for example: model and migration, then service, then API, then tests). Finish and validate each one before starting the next.

## 2. Surgical reading

- Never read a whole file by default. Use search (grep/glob) to locate the spot, then read only the needed range or function.
- Do not re-read a file already read in the conversation, or one you just edited.
- Do not explore dependency, media, build, or cache folders, nor lockfiles (node_modules, .venv, media, coverage, output).
- Before implementing, check what already exists (a short git status/diff, neighboring models and serializers) so finished work is not rewritten.

## 3. Execution

- Make the smallest compatible change (KISS). Reuse existing serializers, services, and patterns.
- Edit with targeted patches; do not rewrite whole files.
- Batch independent tool calls in the same round.
- Do not spawn subagents, write reports, or create extra files unless explicitly asked.

## 4. Loop guard (mandatory)

- At most 3 attempts per error; change the hypothesis on every new attempt. Never repeat the same command expecting a different result.
- If the environment blocks something (network, dependencies, permissions), diagnose ONCE, do not work around it, and report it. Do not burn steps on variations.
- After 3 consecutive steps with no verifiable progress, stop, return a diagnosis, and ask for the missing information.

## 5. Cheap verification

- Ask the user to run tests and lint in their own terminal and paste only the relevant output (the traceback of the first failing test) instead of iterating inside the conversation.
- Validate syntax locally (compile/lint) when the full suite cannot be run.

## 6. Final answer

- One to three sentences of outcome, a short list of changed files, the commands for the user to run, and real pending items. No step-by-step recap.

## Hints to give the user

- Long conversation or new topic: suggest /clear (or /compact to keep the thread).
- Routine task: suggest a lighter model via /model.
- Bloated context: suggest /context to see what is taking space.
