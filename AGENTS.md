# claude-plugins

The `ai-bible` Claude Code plugin marketplace: a curated index of plugins and skills for using AI more effectively.

## Layout

- `.claude-plugin/marketplace.json`: every plugin entry. The marketplace name is `ai-bible`.
- `plugins/<name>/`: plugins authored in this repo, listed with source `./plugins/<name>`.
- Third-party plugins are entries pointing at the author's own repo (`github` or `git-subdir` source); their code is never copied here.

## Conventions

- Every change starts as a GitHub issue and lands as a PR; `main` is protected.
- Every plugin added to the marketplace also gets a line in `README.md`.
- Commits, PRs and issues carry no AI attribution lines.

## Gates

1. `claude plugin validate .`
2. Each plugin added or changed in the branch installs, in a throwaway config so the user's own `ai-bible` setup is untouched: `export CLAUDE_CONFIG_DIR="$(mktemp -d)" && claude plugin marketplace add ./ && claude plugin install <name>@ai-bible`
3. PR body links its issue with `Closes #<n>`
