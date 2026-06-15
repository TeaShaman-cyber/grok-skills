---
name: linear
description: Convenient helpers for working with Linear.app (issues, comments, milestones, updates). Uses grok-mcp under the hood but provides shorter and more intuitive commands.
---

# Linear Skill

This skill provides convenient shortcuts for working with Linear through the connected MCP tools.

## Core Principles

- Always use the shortest intuitive command possible.
- Prefer high-level commands over raw `grok-mcp call linear___...` when possible.
- Always confirm destructive actions (archiving, deleting, changing state to Done/Canceled).

## Available Commands

### Issues

- `linear list [assignee=me] [state=started|backlog|todo|completed] [limit=20]`
  List issues. Default: my active issues.

- `linear get <issueId>`
  Get full details of one issue (LIN-1234 or UUID).

- `linear create title="<title>" [description="..."] [project="Team Name"] [assignee=me] [state=backlog|todo]`
  Create a new issue.

- `linear update <issueId> [title="..."] [description="..."] [state=started|completed|backlog] [assignee=me|<user>]`
  Update an existing issue (title, description, state, assignee).

- `linear comment <issueId> "<text>"`
  Add a comment to an issue.

- `linear comments <issueId> [limit=30]`
  List comments on an issue.

- `linear search "<query>" [limit=20]`
  Search issues by text.

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

- `linear done <issueId>`
  Quickly mark an issue as completed (shortcut for `linear update <id> state=completed`).

## Examples

```bash
# List my current work
linear list assignee=me state=started

# Create a new task
linear create title="Fix login bug" project="Platform" assignee=me

# Update issue status and assignee
linear update LIN-4821 state=started assignee=me

# Quick complete
linear done LIN-4821

# Add a comment
linear comment LIN-4821 "Done with the first part, moving to testing"

# Search issues
linear search "login bug"
```

## Under the Hood

This skill translates high-level commands into the appropriate `grok-mcp call linear___...` calls. It uses the `linear` tools discovered via `grok-mcp ls`.

If a command is not covered here, fall back to direct `grok-mcp` usage after running `grok-mcp ls --query "linear"`.

## Diagnostics & Troubleshooting

Если команды Linear не работают или возвращают ошибки:

1. **Проверь статус MCP**
   ```bash
   grok-mcp check
   ```
   Это покажет, жив ли MCP и есть ли проблемы с аутентификацией.

2. **Посмотри доступные Linear инструменты**
   ```bash
   grok-mcp ls --query "linear"
   ```
   Убедись, что нужный инструмент (например, `linear___update_issue`) присутствует в списке.

3. **Частые проблемы**
   - `issueId` не найден → используй полный UUID или правильный идентификатор (LIN-XXXX).
   - Нет прав на изменение задачи → проверь, что у тебя есть доступ в Linear к этому проекту/команде.
   - Команда не распознаётся → убедись, что skill `linear` активен (он должен быть в `~/.grok/skills/`).

4. **Fallback**
   - Если MCP недоступен, используй веб-интерфейс Linear напрямую.
   - Для срочных задач можно создать issue через веб и потом привязать к разговору.

5. **Полезные команды для диагностики**
   ```bash
   grok-mcp check
   grok-mcp ls --query "linear"
   linear get <issueId>          # проверить, что issue существует
   ```
