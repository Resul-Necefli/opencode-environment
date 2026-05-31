# AGENTS.md

## What this repo is

A multi-agent orchestration environment for the **opencode** tool — NOT a traditional Go application. The `go.mod` and `main.go` are stubs. The real substance is the agent definitions, system prompts, skills, and workflows in the six agent directories.

## Agent pipeline

```
Business Request → plans → task-manager → {db-architect, golang-architect}
                                          → {db-engineer, golang-engineer}
```

- **plans** (primary, `gpt-5`): converts requests into structured plans
- **task-manager** (primary, `gpt-5`): breaks plans into tasks, dispatches to agents
- **db-architect** (subagent, `opencode/gemini-3.1-pro`): designs DB architecture
- **db-engineer** (execution-agent, `gpt-5`): implements `db-architect` output as SQL
- **golang-architect** (subagent, `gpt-5`): designs Go backend architecture
- **golang-engineer** (execution-agent, `gpt-5`): implements `golang-architect` output as Go code

Dependency chains enforced by task-manager: architect → engineer (never the reverse).

## Critical path quirks — typos and mismatches

These are real directory/file names. Do NOT "fix" them without updating all `{file:...}` references in agent configs and system prompts.

- **`skils/`** — every agent directory uses `skils/` (not `skills/`). All `{file:skills/...}` references in prompts point to this misspelled directory.
- **`golang-engineer/workfllow/`** — triple L, not a typo you should silently correct.
- **`db-architect`** uses `prompts/` (plural) and `workflows/` (plural); other agents use `prompt/` and `workflow/` (singular). `task-manager` uses `prompts/` (plural) + `workflow/` (singular).
- **`golang-engineer/prompt/golang-architect.system.md`** — file is misnamed after the architect role, but contains the engineer system prompt.

## Missing but referenced

- `plans/skils/` system prompt references `{file:skills/planning.md}` but only `business-analysis.md` and `system-thinking.md` exist.

## No build/test/lint commands

No Makefile, no CI, no test files, no linter config, no `go.sum`. The Go module has zero external dependencies. `go run main.go` prints `hello agent` and nothing else.

## Permission models differ

- `db-architect`: granular (`question:allow`, `task:deny`, `file_read:allow`, `file_write:deny`)
- All others: single-string (`workspace-write`, `db-write`, `backend-design`, `code-write`)
