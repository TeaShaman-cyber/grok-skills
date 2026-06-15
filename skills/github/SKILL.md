---
name: github
description: Convenient helpers for working with GitHub (pull requests, issues, branches, collaborators, comments). Uses grok-mcp under the hood.
---

# GitHub Skill

This skill provides convenient shortcuts for common GitHub operations through connected MCP tools.

## Core Principles

- Default to the current repository context when possible.
- Prefer read operations by default. Be explicit when doing write operations.
- Always confirm before creating/updating/deleting.

## Available Commands

### Pull Requests

- `github pr list [owner=...] [repo=...] [state=open|closed|all] [author=me]`
  List pull requests.

- `github pr get <number>`
  Get details of one pull request.

- `github pr comments <number>`
  List comments and reviews on a PR.

### Issues

- `github issue list [owner=...] [repo=...] [state=open|closed|all] [assignee=me]`
  List issues.

- `github issue get <number>`
  Get full issue details.

- `github issue comment <number> "<text>"`
  Add a comment to an issue.

### Create & Update

- `github issue create title="<title>" [body="..."] [assignee=me] [labels=...]`
  Create a new issue.

- `github pr create title="<title>" head="<branch>" base="main" [body="..."]`
  Create a Pull Request.

### Branches & Repository

- `github branches [owner=...] [repo=...]`
  List branches.

- `github collaborators [owner=...] [repo=...]`
  List repository collaborators.

### Quick Workflows

- `github my-prs`
  List my open pull requests.

- `github review-queue`
  Show PRs that need my review.

- `github triage [repo=...]`
  Show open issues and PRs that need attention.

## Examples

```bash
# List open PRs
github pr list state=open

# Get PR details
github pr get 42

# Create an issue
github issue create title="Fix login bug" body="Steps to reproduce..." assignee=me

# Add comment to issue
github issue comment 17 "LGTM, let's ship it"

# Create a Pull Request
github pr create title="Add new feature" head="feature/xyz" base="main"
```

## Under the Hood

This skill is a convenience layer over `grok-mcp` tools. Always run `grok-mcp ls --query "github"` first if you need to discover available tools.

## Модули экосистемы GitHub

Дополнительные знания по экосистеме GitHub вынесены в отдельные модули (чتобы ла раздувать этот skill):

- `github/actions.md` — GitHub Actions, workflows, CI/CD
- `github/git-flow.md` — стратегии ветвления и best practices (в разработке)

При необходимости я читаю соответствующий модуль.
