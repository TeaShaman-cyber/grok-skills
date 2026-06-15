---
name: graphql
description: Practical guidance for working with GraphQL APIs, with a focus on Apollo Client caching, query design, and architectural decisions between REST and GraphQL. Helps maintain high coherence and low asymmetry when working with connected services (Linear, GitHub, Notion, etc.).
---

# GraphQL Skill

This skill helps you work effectively with GraphQL APIs — especially when using Apollo Client — while keeping cognitive load low and decisions aligned with TИД principles (high coherence, low asymmetry, natural flow).

## When to Use This Skill

- Choosing between REST and GraphQL for a new integration or feature.
- Designing or reviewing GraphQL queries and mutations.
- Debugging or optimizing Apollo Client caching behavior.
- Working with GraphQL-based connectors (Linear, GitHub, Notion, etc.).
- Wanting to keep data fetching efficient and predictable.

## 1. REST vs GraphQL — Quick Decision Framework

Use this mental model:

**Choose REST when:**
- Resources are relatively independent
- You need strong caching at HTTP level (CDN, browser cache)
- API consumers are simple or you want maximum simplicity
- You have clear, stable resource boundaries

**Choose GraphQL when:**
- Data is highly interconnected (issues ↔ projects ↔ comments, PRs ↔ reviews, etc.)
- Clients often need different combinations of data in one request
- You want to minimize over-fetching and under-fetching
- You work with complex UIs or multiple clients (web + mobile)

**Rule of thumb:**
If you find yourself making multiple REST calls to assemble one view — strongly consider GraphQL.

## 2. Apollo Client Caching (Most Important Practical Part)

Apollo's `InMemoryCache` is powerful but requires understanding.

### Core Concepts

- **Normalization**: Apollo stores objects by `id` + `__typename` by default.
- **Key**: Every object should have a stable, unique `id`.
- **Type Policies**: Custom logic for how specific types are read, merged, and cached.

### fetchPolicy — When to Use What

| Policy              | Use Case                                      | Network | Cache | Recommendation |
|---------------------|-----------------------------------------------|---------|-------|----------------|
| `cache-first`       | Default for most reads                        | No      | Yes   | Default choice |
| `cache-and-network` | When you want fresh data but also instant UI  | Yes     | Yes   | Good for lists that update often |
| `network-only`      | When data must be fresh (mutations aftermath) | Yes     | No    | Use after important mutations |
| `no-cache`          | Fire-and-forget or very dynamic data          | Yes     | No    | Rare |
| `cache-only`        | Purely offline or when you know data exists   | No      | Yes   | Rare, mostly for optimistic UI |

### After Mutations — Update Cache Properly

Never rely on `refetchQueries` as the only strategy. Prefer surgical updates:

```ts
// Good pattern
const [createComment] = useMutation(CREATE_COMMENT, {
  update(cache, { data }) {
    cache.modify({
      id: cache.identify({ __typename: "Issue", id: issueId }),
      fields: {
        comments(existing = []) {
          const newCommentRef = cache.writeFragment({
            data: data.createComment,
            fragment: COMMENT_FRAGMENT,
          });
          return [...existing, newCommentRef];
        },
      },
    });
  },
});
```

### typePolicies — Common Patterns

```ts
const cache = new InMemoryCache({
  typePolicies: {
    Issue: {
      fields: {
        // Always merge comments instead of replacing
        comments: {
          merge(existing = [], incoming) {
            return [...existing, ...incoming];
          },
        },
      },
    },
    Query: {
      fields: {
        // Pagination helper
        issues: {
          keyArgs: ["filter"],
          merge(existing, incoming, { args }) {
            // custom pagination merge logic
          },
        },
      },
    },
  },
});
```

## 3. Practical Patterns

### Prefer fewer, more precise queries

Bad:
```graphql
query GetEverything {
  issue(id: $id) { ... }
  project(id: $projectId) { ... }
  user(id: $userId) { ... }
}
```

Better: one focused query that returns exactly what the component needs.

### Use fragments heavily

```graphql
fragment IssueCard on Issue {
  id
  title
  state { name }
  assignee { id name avatarUrl }
}

query IssueList {
  issues { nodes { ...IssueCard } }
}
```

### Always think about cache invalidation after mutations

After creating/updating/deleting, decide:
- Use `update` for immediate UI consistency (preferred)
- Fall back to `refetchQueries` only when update is too complex

## Connection to TИД and Cognitive Navigation

- High **C** (coherence): Good GraphQL queries + proper caching keep the mental model of data consistent.
- Low **Δf** (asymmetry): Avoiding over-fetching and unnecessary requests reduces friction between what you want and what you get.
- **γ ≈ 1.10**: Efficient GraphQL usage naturally produces a healthier "information noise" profile — enough variety without chaos.

## Anti-patterns to Avoid

- Using `network-only` everywhere "just to be safe"
- Ignoring `typePolicies` when you have custom pagination or merging logic
- Making huge queries "because GraphQL allows it"
- Treating GraphQL as "REST with a single endpoint"

---

Use this skill whenever you design queries, set up Apollo, or decide between REST and GraphQL for a new feature.
