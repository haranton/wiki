---
order: 7
title: codex
---

model = "gpt-5.3-codex"

model_reasoning_effort = "medium"

\[mcp_servers.onecPlatform\]

command = "npx"

args = \["-y", "mcp-remote", "<http://localhost:8001/sse>"\]

\[mcp_servers.onec_server_direct\]

command = "npx"

args = \["-y", "mcp-remote", "<http://localhost/codex/hs/mcp/>"\]


