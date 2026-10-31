---
name: atomic-git-publish
description: Review pending Git changes, organize them into atomic commits, validate them, and push the current branch. Use when the user asks to commit and push work, especially when they request atomic commits, commit descriptions, or omission of co-author trailers.
---

# Atomic Git Publish

Complete the repository handoff rather than only suggesting commands.

1. Read the applicable repository instructions and inspect the repository root, current branch, upstream, status, staged changes, untracked files, and full diffs. Preserve user changes and do not treat the existing staging area as an intentional commit boundary without checking it.
2. Group changes by cohesive responsibility. Each commit should be independently understandable and leave the repository in a sensible state. Keep formatting, generated lockfiles, tests, and documentation with the change they directly support; separate unrelated cleanup or documentation when it has its own purpose.
3. Run `git diff --check` and validations proportional to the changed code before committing. Prefer the project's documented commands. Do not introduce broad fixes solely to clear unrelated pre-existing failures; report those failures accurately.
4. Follow the repository's recent commit convention. Use a concise subject and add a body when the reason, behavior, migration, or tradeoff is not obvious from the subject. Never add `Co-authored-by` or any other co-author footer. Do not rewrite existing commits unless the user explicitly requests it.
5. Stage explicit paths for one group at a time, inspect the staged diff, then commit it. Repeat until all intended changes are committed. Do not include secrets, local environment files, build output, or unrelated files merely because they are present.
6. Verify the new commit messages and bodies, confirm the worktree state, and push the current branch to its configured upstream. An explicit request to commit and push authorizes the normal push. Never force-push unless the user explicitly requests history rewriting.
7. After pushing, verify the branch is synchronized. Report commit hashes and subjects, validation results, and any remaining failures or uncommitted files.

If a normal push is rejected, inspect the remote divergence before acting. Integrate remote changes without discarding local or user work, then retry only when the resolution is clear and within scope.
