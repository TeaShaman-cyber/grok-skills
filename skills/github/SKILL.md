---
name: github
description: Convenient helpers for working with GitHub (pull requests, issues, branches, collaborators). Uses grok-mcp under the hood.
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
  List pull requests. Default: open PRs in current context.

- `github pr get <number>`
  Get details of one pull request.

- `github pr comments <number>`
  List comments/reviews on a PR.

### Issues

- `github issue list [owner=...] [repo=...] [state=open] [assignee=me]`
  List issues.

- `github issue get <number>`
  Get full issue details.

- `github issue comment <number> "<text>"`
  Add a comment to an issue.

### Branches & Repository

- `github branches [owner=...] [repo=...]`
  List branches.

- `github collaborators [owner=...] [repo=...]`
  List repository collaborators.

### Quick Workflows

- `github my-prs`
  List my open pull requests across repositories I have access to.

- `github review-queue`
  Show PRs that need my review (where I am requested as reviewer).

- `github triage [repo=...]`
  Show open issues and PRs that need attention (no assignee, stale, etc.).

## Examples

```bash
# List open PRs in current repo
github pr list state=open

# Get details of PR #42
github pr get 42

# Add a comment to issue #17
github issue comment 17 "LGTM, let's ship it"

# List my open PRs
github my-prs
```

## Under the Hood

This skill is a convenience layer over `grok-mcp` tools:
- `github___list_pull_requests`
- `github___list_issues`
- `github___list_branches`
- `github___list_repository_collaborators`
- etc.

Always run `grok-mcp ls --query "github"` first if you need to discover new or updated tools.
