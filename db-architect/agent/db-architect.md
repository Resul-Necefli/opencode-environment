---
description: "database optimization architect"
mode: subagent
model: "opencode/gemini-3.1-pro"
prompt: "{file:prompts/db-architect.system.md}"
permissions:
  question: allow
  task: deny
  file_read: allow
  file_write: deny
---
