---
name: connectors
description: Helper for navigating connected services (MCP tools). Helps reduce cognitive load by showing what is available and suggesting the right tool for the task. Includes diagnostics and fallback strategies.
---

# Connectors Helper Skill

This skill acts as a navigator and diagnostic tool for all connected services via MCP. Its main goal is to reduce the need to remember specific tool names and to provide quick guidance when working with external services.

## When to Use This Skill

- You don't remember which tool to use for a specific task.
- You want to quickly check what is currently connected and available.
- Something is not working and you need to diagnose the issue.
- You want to understand fallback options when a connector is unavailable.

## Core Commands

### Overview & Diagnostics

- `connectors status`
  Show overall MCP status and list of connected services.

- `connectors list [service]`
  List available tools. If `service` is specified (e.g. `linear`, `github`, `gmail`), filter by it.

- `connectors diagnose [service]`
  Run basic diagnostics for a specific service or all services.

### Quick Guidance

- `connectors suggest "<task description>"`
  Suggest the most appropriate tool(s) for a given task (e.g. "list my open Linear issues", "create GitHub PR").

- `connectors fallback [service]`
  Show what to do if a specific connector is unavailable.

## Examples

```bash
# Check overall status
connectors status

# See all Linear tools
connectors list linear

# Get suggestion for a task
connectors suggest "update Linear issue status to In Progress"

# Diagnose GitHub connector
connectors diagnose github

# What to do if Linear is down
connectors fallback linear
```

## Under the Hood

This skill primarily uses:
- `grok-mcp check`
- `grok-mcp ls`
- `grok-mcp ls --query "<service>"`

It parses the output and presents it in a more human-friendly way with recommendations.

## Diagnostics & Fallback (Core Value)

**If MCP or a connector is not working:**

1. Run:
   ```bash
   connectors status
   connectors diagnose
   ```

2. Common actions:
   - Reconnect the connector in Grok settings (Settings → Connectors).
   - Check OAuth permissions.
   - Use the web interface of the service directly as a temporary fallback.

3. For critical work, always have a manual fallback path (web UI or direct API).

## Philosophy

This skill exists specifically to **reduce cognitive load**. It should answer questions like:
- "What can I do right now?"
- "Which tool should I use?"
- "What if this doesn't work?"

It is intentionally lightweight and focused on navigation and diagnostics rather than replacing the underlying tools.
