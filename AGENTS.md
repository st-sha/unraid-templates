<!-- agent-standards v1.1-draft, profile: light -->
# unraid-templates

Rules for coding agents working in this repo. They add to Steven's personal rules from the
agent-standards plugin. Where the two differ, this file wins.

## Purpose

Unraid Docker templates for Steven's containers (today: CubeMan.xml). Unraid's Community Apps
reads the template XML files from the default branch, so `main` is live.

## Commands and tools

- setup: none.
- check: `pwsh -NoProfile -Command '$ErrorActionPreference = "Stop"; Get-ChildItem -Filter *.xml | ForEach-Object { [xml](Get-Content -Raw $_.FullName) | Out-Null; "ok " + $_.Name }'`
  (run from pwsh; parses every template XML at the root and exits 1 on the first one that is not
  well-formed).
- run: none. Unraid installs the templates; nothing runs locally.
- MCP servers kept on: none. The rest are off in `.github/copilot/settings.json`. Name each kept server in backticks; a reason may follow it.

## Workflow

- Work in a session worktree on a branch. Never edit the main checkout.
- Commit in small, logical steps. Stage files by name.
- Push and merge: push the branch to origin and open a PR on st-sha/unraid-templates. Steven
  merges. Merging to `main` publishes the templates to Community Apps.
- Don't rename, move or reformat template XML. Any new file that is not a template must not end
  in `.xml`, or Community Apps may read it as one.

## Safety

- Ask Steven first before: merging or pushing to `main`; renaming, moving or deleting a template;
  changing a template's image, ports or paths; adding a new `.xml` file; adding CI.
- Secrets never go in the repo. Local values live in `.env`, which git ignores.

## Deviations

None. Add one line per deviation from the standard, in this form:
`- <check>: <reason>. Added YYYY-MM-DD; revisit by YYYY-MM-DD.`
`<check>` is a check id from STANDARD.md section 3, such as `plan` or `settings`.
