# AGENTS.md

## What this repo is

A multi-agent orchestration environment for the **opencode** tool. The `go.mod` and `main.go` are stubs. The real substance is the agent definitions, skills, and workflows.

## OpenCode discovery structure

Agents and skills are registered via the standard OpenCode discovery paths. **Do not** put agent configs in the root-level `<name>/<name>.md` directories — OpenCode will not find them there.

### Canonical paths

| What | Path |
|---|---|
| Project config | `opencode.json` |
| Agent definitions | `.opencode/agent/<name>.md` |
| Skills | `.opencode/skill/<name>/SKILL.md` |
| Global instructions | `opencode.json` → `instructions` array |

### Original directories (kept as reference)

The root-level `plans/`, `task-manager/`, `db-architect/`, `db-engineer/`, `golang-architect/`, `golang-engineer/` directories are **reference only** — they contain the raw prompts, skills, and workflows that were migrated into `.opencode/`. Do not edit them expecting OpenCode to pick up changes.

## Agent pipeline

```
Business Request → plans → task-manager → {db-architect, golang-architect}
                                          → {db-engineer, golang-engineer}
```

- **plans** (primary, `gpt-5`): converts requests into structured plans
- **task-manager** (primary, `gpt-5`): breaks plans into tasks, dispatches to agents
- **db-architect** (subagent, `opencode/gemini-3.1-pro`): designs DB architecture
- **db-engineer** (subagent, `gpt-5`): implements `db-architect` output as SQL
- **golang-architect** (subagent, `gpt-5`): designs Go backend architecture
- **golang-engineer** (subagent, `gpt-5`): implements `golang-architect` output as Go code

Dependency chains enforced by task-manager: architect → engineer (never the reverse).

## How edits propagate

- **Agent prompts**: edit `.opencode/agent/<name>.md` (the file body IS the prompt)
- **Skills**: edit `.opencode/skill/<name>/SKILL.md`
- **Workflows**: referenced in `opencode.json` → `instructions` array; edit the `workflow/` files in the original directories
- **After any config change**: quit and restart `opencode` for changes to take effect

## Permissions

- **plans**: `edit: allow, bash: allow`
- **task-manager**: `edit: allow, bash: allow`
- **db-architect**: `question: allow, task: deny, read: allow, edit: deny, bash: deny`
- **db-engineer**: `edit: allow, bash: psql * allow / * ask`
- **golang-architect**: `edit: ask, bash: ask`
- **golang-engineer**: `edit: allow, bash: allow`

## No build/test/lint commands

No Makefile, no CI, no test files, no linter config, no `go.sum`. `go run main.go` prints `hello agent` and nothing else.

## Original directory quirks (reference only)

These are real directory/file names in the reference directories. Do NOT "fix" them.

- **`skils/`** — misspelled, used consistently across all agent dirs
- **`golang-engineer/workfllow/`** — triple L
- **`db-architect`** uses `prompts/` (plural) and `workflows/` (plural); other agents vary
- **`golang-engineer/prompt/golang-architect.system.md`** — misnamed after the architect role

## Missing but referenced

- `plans/skils/` system prompt references `{file:skills/planning.md}` but only `business-analysis.md` and `system-thinking.md` exist. This is in the original reference dir — the `.opencode/` agents no longer use `{file:...}` syntax.