# Project Context for AI Agents

## What this repo is

This is Continuous Networks' **fork** of `intuitem/ciso-assistant-community`. Upstream is the authoritative source — we only track it to enable future customizations.

Current state: **no customizations applied**. Fork is clean and in sync with upstream.

## Remotes

- `origin` → `Continuous-Networks/ciso-assistant-community` (our fork on GitHub)
- `upstream` → `intuitem/ciso-assistant-community` (the source project)

## Golden rules

- **Never modify `main` directly.** It's a clean mirror of upstream. Customizations live on branches.
- **Never push to `upstream`.** We don't have write access and shouldn't want it. Use PRs if contributing back.
- **The MCP server code lives in `cli/ca_mcp/`.** Don't touch anything outside that directory for CN-specific customizations unless there's a very good reason.

## Syncing with upstream (weekly / monthly)

```bash
git checkout main
git pull upstream main
git push origin main
```

If you're on a customization branch, merge main into it afterward:

```bash
git checkout cn/custom-tools   # or whatever branch name
git merge main
# resolve any conflicts, commit
git push origin cn/custom-tools
```

## Adding a customization (future)

1. `git checkout main && git pull upstream main` — start from latest upstream
2. `git checkout -b cn/<descriptive-name>` — create a branch
3. Make changes — ideally only in `cli/ca_mcp/`
4. Before writing a new tool: **grep upstream first** to check if the tool now exists. Example: `grep -rn "def get_<tool_name>" cli/ca_mcp/`
5. Commit, push to `origin`
6. Document the customization at the bottom of this file so future-you knows what's on this branch and why

## Historical customizations (removed)

- **`get_vulnerabilities`** — Added April 2026 to a stale local copy. Upstream shipped an equivalent implementation in v3.15.2 (PR #3732). Custom version deleted; upstream is sufficient.
- **`update_requirement_assessments`** — Previously added. Verify upstream status before re-adding.

## Deployment

Production CISO Assistant runs on the Proxmox LXC via Docker Compose from the upstream `docker-compose.yml`. The MCP server is invoked via LM Studio's `mcp.json` config. Secrets (API keys, base URLs) live in LM Studio's MCP configuration, NOT in this repo. Do not commit any `mcp.json` or credential files into this fork.

## Active customizations

_None currently. Document any added here with: branch name, what it does, why upstream doesn't meet the need, and the date added._
