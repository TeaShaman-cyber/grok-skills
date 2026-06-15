---
name: linear
description: Convenient helpers for working with Linear.app (issues, comments, milestones). Uses grok-mcp under the hood but provides shorter and more intuitive commands.
---

# Linear Skill

This skill provides convenient shortcuts for working with Linear through the connected MCP tools.

## Core Principles

- Always use the shortest intuitive command possible.
- Prefer high-level commands over raw `grok-mcp call linear___...` when possible.
- Always confirm destructive actions (archiving, deleting, changing state to Done/Canceled).

## Available Commands

### Issues

- `linear list [assignee=me] [state=started|backlog|todo] [limit=20]`
  List issues. Default: my active issues.

- `linear get <issueId>`
  Get full details of one issue (LIN-1234 or UUID).

- `linear comment <issueId> "<text>"`
  Add a comment to an issue.

- `linear comments <issueId> [limit=30]`
  List comments on an issue.

### Milestones / Projects

- `linear milestones [project="Team Name"]`
  List milestones for a project.

- `linear milestone <id>`
  Get details of one milestone.

### Quick Workflows

- `linear my-week`
  Show my issues that are in progress or need attention this week.

- `linear triage`
  Show issues that are in backlog/triage and need prioritization.

## Examples

```bash
# List my current work
linear list assignee=me state=started

# Add a quick comment
linear comment LIN-4821 "Done with the first part, moving to testing"

# See comments on an issue
linear comments LIN-4821

# List milestones for a specific project
linear milestones project="Q3 Platform"
```

## Under the Hood

This skill translates high-level commands into the appropriate `grok-mcp call linear___...` calls. It uses the `linear` tools discovered via `grok-mcp ls`.

If a command is not covered here, fall back to direct `grok-mcp` usage after running `grok-mcp ls --query "linear"`.
