# GraphQL

> A query language for your API. Ask for what you need, get exactly that.

---

## Purpose

Master GraphQL: schema, resolvers, queries, mutations, subscriptions, federation.

## Prerequisites

- [APIs/](../APIs/), [REST/](../REST/).

## Learning Outcome

You can design a GraphQL schema, write resolvers, and ship a GraphQL API.

## Dependencies

- Backend framework.

## Related Files

- [APIs/](../APIs/) · [REST/](../REST/) · [GraphQL/schema.md](schema.md) · [GraphQL/resolvers.md](resolvers.md) · [GraphQL/federation.md](federation.md)

## AI Instructions

When building GraphQL:
1. **Schema-first** design.
2. **Strong typing** (built-in).
3. **Resolvers** per field.
4. **DataLoader** to avoid N+1.
5. **Persisted queries** for production.
6. **Rate limit** by query cost, not request count.
7. **Disable introspection** in production (or behind auth).
8. **Cache** at the field level where possible.

## Human Notes

### Schema
```graphql
type User {
  id: ID!
  name: String!
  email: String!
  posts: [Post!]!
}

type Post {
  id: ID!
  title: String!
  author: User!
}

type Query {
  user(id: ID!): User
  users(limit: Int = 10, cursor: String): UserConnection!
}

type Mutation {
  createUser(input: CreateUserInput!): User!
}

type Subscription {
  postAdded: Post!
}

input CreateUserInput {
  name: String!
  email: String!
}

type UserConnection {
  edges: [UserEdge!]!
  pageInfo: PageInfo!
}

type UserEdge {
  node: User!
  cursor: String!
}

type PageInfo {
  hasNextPage: Boolean!
  endCursor: String
}
```

### Queries
```graphql
query GetUser($id: ID!) {
  user(id: $id) {
    id
    name
    posts {
      id
      title
    }
  }
}
```

### Mutations
```graphql
mutation CreateUser($input: CreateUserInput!) {
  createUser(input: $input) {
    id
    name
  }
}
```

### Subscriptions
Real-time via WebSocket.
```graphql
subscription {
  postAdded {
    id
    title
  }
}
```

### Resolvers
```js
const resolvers = {
  Query: {
    user: async (_, { id }, { db }) => db.user.findUnique({ where: { id } }),
  },
  User: {
    posts: async (parent, _, { db }) => db.post.findMany({ where: { authorId: parent.id } }),
  },
};
```

### N+1 problem
Each `User.posts` resolver fires per user. With 100 users = 100 queries.

Fix with DataLoader:
```js
import DataLoader from 'dataloader';

const postsLoader = new DataLoader(async (userIds) => {
  const posts = await db.post.findMany({ where: { authorId: { in: userIds } } });
  return userIds.map(id => posts.filter(p => p.authorId === id));
});

const resolvers = {
  User: {
    posts: (parent) => postsLoader.load(parent.id),
  },
};
```

### Federation
Multiple services expose GraphQL schemas, composed into one supergraph.
- Apollo Federation.
- For microservices.

→ [GraphQL/federation.md](federation.md)

### Authentication
- Same as REST: bearer token in `Authorization` header.
- Pass user via context.

### Rate limiting
- Not by request count (one query can be 100x another's cost).
- Use query cost analysis (persisted queries + cost limits).

### Caching
- GET-like queries can be HTTP-cached.
- Apollo Client caches client-side.
- Server-side: field-level resolvers can cache.

### Security
- Disable introspection in production (or auth-gate it).
- Query depth limiting (prevent DoS).
- Query complexity analysis.
- Persisted queries only (predefined, no client-defined queries).

## Common Mistakes

- ❌ N+1 queries.
- ❌ No persisted queries (DoS surface).
- ❌ No depth/complexity limits.
- ❌ Exposing DB schema directly.
- ❌ Versioning via schema changes that break clients.
- ❌ Using GraphQL for file uploads (use REST instead).

## Tools

- Apollo Server: https://www.apollographql.com/docs/apollo-server/
- GraphQL Yoga: https://the-guild.dev/graphql/yoga-server
- Pothos (type-safe schema builder): https://pothos-graphql.dev/
- Apollo Client: https://www.apollographql.com/docs/react/
- urql: https://github.com/urigo/urql
- Relay: https://relay.dev/
- GraphQL Mesh: https://www.graphql-mesh.com/
- GraphQL Code Generator: https://the-guild.dev/graphql/codegen

## References

- GraphQL spec: https://spec.graphql.org/
- GraphQL.org: https://graphql.org/
- Apollo docs: https://www.apollographql.com/docs/
- How to GraphQL: https://www.howtographql.com/

## Further Reading

- *The Road to GraphQL* — Robin Wieruch
- *Production-Ready GraphQL* — Marc-André Giroux

## Exercises

1. Build a GraphQL API for a blog.
2. Add DataLoader to fix N+1.
3. Add subscriptions for real-time comments.

## Projects

- Build a federated GraphQL API across 3 services.
- Build a GraphQL BFF (backend for frontend) for a mobile app.

---

**Previous:** [REST/](../REST/) · **Next:** [WebSockets/](../WebSockets/) · **Related:** [APIs/](../APIs/)
