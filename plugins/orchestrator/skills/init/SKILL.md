---
name: init
description: Create the repo's AGENTS.md, or add its Gates section, so the orchestrator knows what done means.
disable-model-invocation: true
---
You set up the repo's **gates**: the checks every branch must pass before it becomes a PR.

1. **Look.** Check the repo root for `AGENTS.md` and `CLAUDE.md`. `AGENTS.md` that already has a `## Gates` section: tell the user the repo is set up and stop.

2. **Research.** Spawn `orchestrator:researcher` to find the commands that prove a branch is healthy: tests, typecheck, lint, format check, build. Sources: `package.json` scripts, `Makefile`, `pyproject.toml`, `Cargo.toml`, `.github/workflows/*`. Without `AGENTS.md`, also ask for the stack, the layout of the main folders and conventions a newcomer would trip over. Ask for exact commands, as CI runs them.

3. **Draft.**
   - No `AGENTS.md`: write the whole file: a one-line purpose, stack, commands, conventions, then `## Gates`.
   - `AGENTS.md` without gates: append only the `## Gates` section and leave every existing line as it is.

   Gates format: a numbered list. An item with a backtick command must exit 0. An item without one is a rule the reviewer checks (for example `PR links its issue with Closes #<n>`).

4. **Load it.** A `CLAUDE.md` exists and lacks an `@AGENTS.md` line: add `@AGENTS.md` at its top, since Claude Code reads `AGENTS.md` itself only when no `CLAUDE.md` exists.

5. **Confirm.** Show the user the gates and the diff. On their OK, spawn `orchestrator:chore` to create branch `chore/agents-md`, commit, push the branch and open a PR. Give the user the PR link.
