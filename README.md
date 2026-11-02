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

This repo vendors nothing. Each entry points at the author's own repository,
so you always get their latest version and their license applies.

## Adding a plugin

All changes go through issues and pull requests; `main` is protected.

1. [Open an issue](../../issues/new?template=add-plugin.yml) suggesting the plugin.
2. Open a PR that adds its entry to `.claude-plugin/marketplace.json` and the README, and links the issue.
3. CI runs `claude plugin validate .`; it must pass before merging. Run it locally first:

```bash
claude plugin validate .
```
