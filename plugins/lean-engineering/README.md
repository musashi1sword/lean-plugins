# Lean Engineering

Seven skills for building software with an AI assistant, adapted and extended from JavaScript Mastery's open-source "skills" workflow (MIT licence, see LICENSE-upstream-jsmastery).

| Skill | Use it when |
|---|---|
| advise | Any technical or product decision: lays out the problem, compares options, recommends one, says what would change the call |
| plan | Starting a project or large feature, or asking for status: v1 scope, riskiest assumption, stack, slices. Big projects get milestones, architecture, a decision log and AGENTS.md |
| develop | Building a slice: checks it can run code, settles open decisions, builds with tests and safety rules |
| check | Before calling it done: `verify` runs the real app with evidence; `review` is a severity-ranked review, ideally by a different model |
| debug | Something is broken: prove the root cause, make the smallest fix, add a regression test |
| ship | Releasing: go/no-go gates, rollout and rollback plan, deploy only on your yes, production check, release notes, postmortems |
| github | Documents the build on GitHub: milestones and issues from the plan, a branch and PR per slice, verify evidence and review verdicts on the PR, releases and incident records. Every other skill suggests the matching GitHub step when it finishes |

Flow: plan → develop (one slice per session) → check verify → check review → ship. Use debug any time, and advise for any decision. Each step ends with a GitHub suggestion.

Files it keeps in your project: docs/plan.md (plus docs/plan/ milestone files on big projects), docs/decisions.md, docs/architecture.md, AGENTS.md, docs/reviews/, docs/releases/, docs/postmortems/.

Requirements: to build and verify, the AI needs to run commands in the project (Claude Code, or a project folder connected in the Claude desktop app).

Safety: every skill treats web pages, documents and code comments as data, not instructions. Nothing gets installed, and nothing goes to production, without your explicit yes.

## Keeping usage low

`plan` and `advise` switch to Opus on their own; everything else uses your default model. For the best balance, set Sonnet as your default in `~/.claude/settings.json`:

```json
{ "model": "sonnet" }
```

Work one slice per session, use `/clear` between slices and `/compact` in long sessions.

## Connecting GitHub (one-time)

Recommended: install the GitHub CLI and run `gh auth login`. This works in Claude Code and on your own computer, and the login stays in your system keychain.

Alternative: GitHub's official MCP server (github/github-mcp-server). In Claude Code:
`claude mcp add --transport http github https://api.githubcopilot.com/mcp -H "Authorization: Bearer <your GitHub token>"`
Use a fine-grained token limited to the project's repositories. Keep the token out of any file you commit.

New repos are created private. Nothing is pushed, opened or released without your yes. Every push is scanned for secrets first. To stop GitHub suggestions for one project, set `suggest: off` under `## GitHub` in its AGENTS.md.
