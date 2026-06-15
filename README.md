# Grok Skills

Custom skills for Grok that improve productivity when working with connected services and maintaining structured research workflows.

## Available Skills

### 1. `linear` — Linear.app Helpers

Convenient shortcuts for working with Linear issues, comments, and milestones.

**Examples:**

```bash
# List my active issues
linear list assignee=me state=started

# Add a quick comment
linear comment LIN-4821 "Done with the first part, moving to testing"

# View comments on an issue
linear comments LIN-4821

# List milestones for a specific project
linear milestones project="Q3 Platform"
```

### 2. `github` — GitHub Helpers

Convenient shortcuts for pull requests, issues, branches, and collaborators.

**Examples:**

```bash
# List open PRs
github pr list state=open

# Get details of a specific PR
github pr get 42

# List my open PRs across all repos
github my-prs

# Show PRs that need my review
github review-queue
```

### 3. `graphql` — GraphQL & Apollo Client

Practical guidance for working with GraphQL APIs, with strong focus on Apollo Client caching, query design, and architectural decisions.

**Key topics covered:**
- When to choose GraphQL vs REST
- Apollo `fetchPolicy` strategies
- Proper cache updates after mutations (`update` vs `refetchQueries`)
- `typePolicies` and normalization best practices
- Connection to TИД principles (coherence, asymmetry, cognitive flow)

Use this skill when designing queries, setting up Apollo, or making architectural decisions about data fetching.

### 4. `tid-methodology` — Theory of Dynamic Measurement

Maintains methodology, file discipline, and iteration process for work on ТИД (Theory of Dynamic Measurement).

**When to activate:**
- Starting a new research iteration
- Performing checkpoints or clean-ups
- Long deep work sessions (> 90 min)
- When deciding what belongs in Research Log vs main theory file

This skill enforces structure and reduces context entropy during complex research work.

## Common Errors & Solutions

### Linear

**Error:** `linear___list_comments` returns empty or error
**Solution:** Make sure you pass the correct `issueId` (e.g. `LIN-1234` or full UUID). Use `linear get <id>` first to verify the issue exists.

**Error:** Comments not appearing after `linear comment`
**Solution:** The comment was added, but the UI cache in Linear may need a refresh. Use `linear comments <id>` to verify, or check the issue in the web UI.

### GitHub

**Error:** `github___list_pull_requests` returns 404 or empty
**Solution:** Check that `owner` and `repo` are correct. For organization repos, you may need to specify `organization` or use the correct team permissions.

**Error:** Cannot create/update files via skill
**Solution:** The GitHub connector may have limited permissions. Check OAuth scopes or use `github___create_or_update_file` directly with proper authentication.

### GraphQL / Apollo

**Error:** Data not updating after mutation
**Solution:** You are probably missing the `update` function in the mutation. Prefer surgical cache updates over `refetchQueries` for better UX.

**Error:** Apollo returns old/stale data
**Solution:** Switch `fetchPolicy` to `cache-and-network` or `network-only` for that specific query. Check your `typePolicies` merge logic.

**Error:** Normalized cache shows duplicate objects
**Solution:** Your objects are missing stable `id` fields or `typePolicies` are not configured correctly for that type.

### General / MCP

**Error:** `grok-mcp ls` shows no tools for a connected service
**Solution:** Run `grok-mcp check` first. Sometimes the connection needs to be re-authenticated or the connector restarted.

**Error:** Tool calls fail with permission errors
**Solution:** Reconnect the connector with broader OAuth scopes, or check the specific permission requested by the tool.

## Installation

These skills are designed to be placed in your `~/.grok/skills/` or project-level `.grok/skills/` directory.

You can clone this repository and symlink or copy the `skills/` folder.

```bash
# Example: symlink into your home grok skills directory
git clone https://github.com/TeaShaman-cyber/grok-skills.git
ln -s $(pwd)/grok-skills/skills/* ~/.grok/skills/
```

## Philosophy

These skills follow the principles of:
- **High coherence** with low unnecessary asymmetry
- **U-wéi** approach to tooling (minimum friction, maximum flow)
- Practical utility over theoretical purity
- Tight integration with TИД methodology

## Contributing

Feel free to open issues or pull requests if you have improvements or additional skills that fit this philosophy.

## License

MIT
