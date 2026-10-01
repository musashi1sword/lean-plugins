# Changelog

## lean-engineering 0.3.0 (beta)

- `plan` and `advise` run on Opus automatically (skill-level `model: opus`); the other skills use your session's default model
- New "Token budget" section in every skill: one slice per session, `/clear` between slices, `/compact` after finished items, read only what the task needs
- Tip: set `"model": "sonnet"` in `~/.claude/settings.json` so routine work defaults to Sonnet

## lean-engineering 0.2.0 (beta)

- Seven skills: advise, plan, develop, check, debug, ship, github
- GitHub checkpoint suggested at the end of every skill
- Safety rules in every skill: untrusted content is data, approval before installs, pushes and deploys, secrets by name only
- Big-project mode in plan: milestones, architecture page, decision log, AGENTS.md
