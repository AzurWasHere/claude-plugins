# claude-plugins

A curated bible of Claude Code plugins and skills for using AI more effectively.
One marketplace, install whatever you need.

## Install

```bash
claude plugin marketplace add AzurWasHere/claude-plugins
```

Then install any plugin by name:

```bash
claude plugin install ponytail@ai-bible
```

Or inside Claude Code: `/plugin` → browse the `ai-bible` marketplace.

## What's inside

### Productivity

| Plugin | What it does | Source |
|---|---|---|
| `ponytail` | Lazy senior dev mode: the smallest change that fully solves the task. | [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail) |
| `caveman` | Talk like caveman. Cut filler, keep technical details. Fewer tokens. | [JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman) |

### Engineering

| Plugin | What it does | Source |
|---|---|---|
| `mattpocock-skills` | Skills for real engineers: grilling, TDD, code review, domain modelling, prototyping. | [mattpocock/skills](https://github.com/mattpocock/skills) |
| `orchestrator` | Opus orchestrator that works GitHub issues end to end across Haiku, Sonnet, Opus and Fable agents. | [this repo](plugins/orchestrator) |

#### orchestrator

Requires `mattpocock-skills` (for grilling) and the `gh` CLI.

| Agent | Model | Job |
|---|---|---|
| `orchestrator` | Opus | Plans, reads criteria from the issue, delegates, never edits |
| `builder` | Opus | Complex code and all UI functionality |
| `stylist` | Fable | Visual polish only; hands behaviour changes back |
| `executor` | Sonnet | Up to 10 files following an existing pattern |
| `researcher` | Sonnet | Read-only investigation |
| `reviewer` | Sonnet | PASS/FAIL per acceptance criterion |
| `chore` | Haiku | CLI, `gh`/`git`, gates, issues, branches, PRs |

1. `/orchestrator:init` once per repo: writes `AGENTS.md`, or adds its `## Gates` section, and opens a PR.
2. `/orchestrator 12 15 18`: issues with an `## Acceptance criteria` checklist start at once, each as a background agent in its own worktree. Issues without one, or `/orchestrator` with no numbers, get grilled first and filed as issues.
3. Each issue runs: build → polish (UI only) → every gate → review → one PR (`Closes #<n>`). One failure escalates the fix a tier: Haiku → Sonnet → Opus → you.

Questions from a background agent come to you in the main session; your answer goes back to that agent. You merge; agents never push to the default branch.

For a whole session as the orchestrator: `claude --agent orchestrator:orchestrator`.

### Security (Trail of Bits suite)

All plugins from [trailofbits/skills](https://github.com/trailofbits/skills), installable one by one.
Highlights:

- `audit-context-building` – map a codebase before hunting bugs
- `static-analysis` – CodeQL, Semgrep and SARIF parsing
- `differential-review` – security review of code changes
- `variant-analysis` – find similar bugs across a codebase
- `insecure-defaults`, `sharp-edges` – footgun and bad-default detection
- `supply-chain-risk-auditor` – npm/PyPI/Go dependency risk
- `c-review`, `rust-review` – language-specific security review
- `building-secure-contracts` – smart contract security toolkit
- `fp-check` – false-positive verification for findings

See [`.claude-plugin/marketplace.json`](.claude-plugin/marketplace.json) for the full list.

## How this works

Third-party plugins are not copied here. Each entry points at the author's own repository,
so you always get their latest version and their license applies.
Plugins authored here live in [`plugins/`](plugins).

## Adding a plugin

All changes go through issues and pull requests; `main` is protected.

1. [Open an issue](../../issues/new?template=add-plugin.yml) suggesting the plugin.
2. Open a PR that adds its entry to `.claude-plugin/marketplace.json` and the README, and links the issue.
3. The branch must pass every gate in [`AGENTS.md`](AGENTS.md). CI runs `claude plugin validate .`; run it locally first:

```bash
claude plugin validate .
```
