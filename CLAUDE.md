# Project Instructions for AI Agents

This file provides instructions and context for AI coding agents working on this project.

<!-- BEGIN BEADS INTEGRATION v:1 profile:minimal hash:6cd5cc61 -->
## Beads Issue Tracker

This project uses **bd (beads)** for issue tracking. Run `bd prime` to see full workflow context and commands.

### Quick Reference

```bash
bd ready              # Find available work
bd show <id>          # View issue details
bd update <id> --claim  # Claim work
bd close <id>         # Complete work
```

### Rules

- Use `bd` for task tracking in this repo — prefer it over ephemeral `TodoWrite`/`TaskCreate` for multi-step or cross-session work. A **GitHub Issue stays the shippable unit** (branch → PR → `Fixes #N`); beads are the execution layer underneath.
- Run `bd prime` for the full command reference.
- Use `bd remember` for **repo-scoped** knowledge that should travel with this repo. Cross-repo / user-level context still lives in the global Claude memory system — `bd remember` does **not** replace it.

**Architecture in one line:** issues live in a local Dolt DB; sync uses `refs/dolt/data` on your git remote; `.beads/issues.jsonl` is a passive export. See https://github.com/gastownhall/beads/blob/main/docs/SYNC_CONCEPTS.md for details and anti-patterns.

## Session Completion

> **Reconciled with the `git-policies` skill.** Beads guards durability/sync; git-policies governs what lands on `main`. **This repo auto-merges** — decided 2026-08-25: there is no required-review gate on `main` here, so opening a PR and leaving it open accomplishes nothing that merging directly doesn't; docs-only changes ship once self-reviewed.

When ending a work session:

1. **File follow-ups** — beads for sub-tasks; a GitHub issue for anything shippable.
2. **Run quality gates** (if content/config changed) — lint, build.
3. **Update bead status** — close finished beads, update in-progress ones.
4. **Make work durable:**
   ```bash
   git add <files> && git commit -S -m "..."   # signed, per git-policies
   git push -u origin <feature-branch>          # push the FEATURE branch
   bd dolt push                                 # sync beads state (refs/dolt/data)
   ```
5. **Open the PR** — `Fixes #N`, `--assignee J-MaFf`, label; self-review the diff, fix anything found.
6. **Squash-merge to `main`** once self-review is clean. No waiting on human approval for this repo — merge as part of finishing the session, not a separate step someone else triggers.

See the `git-policies` skill for the underlying issue → branch → PR → squash-merge mechanics; the auto-merge decision above is this repo's override of that skill's default "leave open for human review" behavior.
<!-- END BEADS INTEGRATION -->


## Build & Test

_Add your build and test commands here_

```bash
# Example:
# npm install
# npm test
```

## Architecture Overview

_Add a brief overview of your project architecture_

## Conventions & Patterns

_Add your project-specific conventions here_
