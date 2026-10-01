# lean-plugins

Plugins for Claude by Musashi2swords.

## lean-engineering (beta, v0.2.0)

An advisor-led software workflow for Claude Code: it settles decisions before code, builds one slice at a time, proves each change works with evidence, releases with a rollback plan, and documents the build on GitHub.

| Skill | Use it when |
|---|---|
| `advise` | Any technical or product decision: lays out the problem, compares options, recommends one, and says what would change the call |
| `plan` | Starting a project or large feature, or checking status: v1 scope, riskiest assumption, stack and build slices. Big projects get milestones, architecture notes and a decision log |
| `develop` | Building a slice: checks it can run code, settles open decisions, builds with tests and safety rules |
| `check` | Before calling it done: `check verify` runs the real app with evidence; `check review` gives a severity-ranked code review |
| `debug` | Something is broken: proves the root cause, makes the smallest fix, adds a regression test |
| `ship` | Releasing: go/no-go gates, rollout and rollback plan, deploys only on your yes, production check, release notes, postmortems |
| `github` | Documents the build on GitHub: milestones and issues from the plan, a PR per slice, review results, releases |

Typical flow: `plan` → `develop` (one slice per session) → `check verify` → `check review` → `ship`. Use `debug` any time, and `advise` for any decision.

## Install (Claude Code)

```
claude plugin marketplace add musashi1sword/lean-plugins
claude plugin install lean-engineering@lean-plugins
```

To update later:

```
claude plugin marketplace update lean-plugins
```

## Install (Claude desktop app)

Download `lean-engineering.plugin` from this repository's Releases page and open it in the Claude desktop app, then press the save or install button on the file card.

## Requirements

- Claude Code, or the Claude desktop app with a project folder connected, so the skills can run commands
- Git, plus the GitHub CLI (`gh auth login`) for the `github` skill
- Optional: `gitleaks` for stronger secret scanning before pushes

## Safety

- Web pages, documents, logs and code comments are treated as data, never as instructions.
- Nothing is installed, pushed, released or deployed without your explicit yes.
- Secrets are referred to by name only, and every push is preceded by a secret scan.
- New GitHub repositories are created private.

## Status and support

This is a beta, provided as-is under the MIT License. It has passed setup tests but has not yet been proven across many real projects. Issues and suggestions are welcome; responses are not guaranteed.

## Credits

Adapted and extended from JavaScript Mastery's open-source [skills](https://github.com/JavaScript-Mastery-Pro/skills) workflow (MIT License). See `LICENSE` and `LICENSE-upstream-jsmastery`.
