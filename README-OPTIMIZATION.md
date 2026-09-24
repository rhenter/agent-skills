# Context optimization

This version reduces unnecessary Codex context usage by:
- moving always-on KISS / Clean Code / Zen principles to `AGENTS.md`;
- narrowing skill descriptions to reduce accidental activation;
- removing repeated generic instructions from every skill;
- making review skills explicitly review-oriented;
- keeping each skill concise.

## Suggested update

Copy `AGENTS.md` to `~/.codex/AGENTS.md`.

Replace the repository `skills/` directory with this optimized `skills/` directory, then:

    git checkout -b optimize-codex-context
    git add AGENTS.md skills
    git commit -m "Optimize agent skills context usage"
    git push -u origin optimize-codex-context
