# Prisma

> Type-safe ORM for Node.js + TypeScript. Schema, migrations, studio, query builder.

---

## Purpose

Use Prisma for type-safe database access in TS/JS apps.

## Prerequisites

- [TypeScript/](../TypeScript/), [Databases/](../Databases/), [PostgreSQL/](../PostgreSQL/) (or another DB).

## Learning Outcome

You can use Prisma to model, migrate, query, and manage a DB.

## Dependencies

- Node.js, Prisma CLI.

## Related Files

- [Drizzle/](../Drizzle/) · [ORM/](../ORM/) · [PostgreSQL/](../PostgreSQL/) · [Databases/](../Databases/)

## AI Instructions

When using Prisma:
1. Use Prisma 5+.
2. Define schema in `schema.prisma`.
3. Use `prisma migrate dev` for dev, `prisma migrate deploy` for prod.
4. Use Prisma Client for queries.
5. Use `select` to avoid over-fetching.
6. Use `include` / `select` to avoid N+1.
7. Use transactions for multi-step writes.
8. Use Prisma Studio for inspection.
9. Use Prisma Accelerate for edge cache (paid).

## Human Notes

### Schema
```prisma
// schema.prisma
generator client { provider = "prisma-client-js" }

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id        Int      @id @default(autoincrement())
  email     String   @unique
  name      String?
  posts     Post[]
  createdAt DateTime @default(now())
}

model Post {
  id        Int      @id @default(autoincrement())
  title     String
  body      String
  author    User     @relation(fields: [authorId], references: [id])
  authorId  Int
  createdAt DateTime @default(now())
}
```

### Migrations
```bash
npx prisma migrate dev --name init
npx prisma migrate deploy  # prod
npx prisma generate  # regenerate client after schema change
npx prisma studio  # GUI
```

### Queries
```ts
import { PrismaClient } from '@prisma/client';
const prisma = new PrismaClient();

// Create
const user = await prisma.user.create({
  data: { email: 'a@b.com', name: 'Alice' },
});

// Read
const user = await prisma.user.findUnique({ where: { id: 1 } });
const users = await prisma.user.findMany({ where: { name: { contains: 'a' } } });

// Update
await prisma.user.update({ where: { id: 1 }, data: { name: 'Bob' } });

// Delete
await prisma.user.delete({ where: { id: 1 } });

// Relations
const userWithPosts = await prisma.user.findUnique({
  where: { id: 1 },
  include: { posts: true },
});

// Select specific fields
const userEmail = await prisma.user.findUnique({
  where: { id: 1 },
  select: { email: true },
});

// Transactions
await prisma.$transaction([
  prisma.user.create({ data: { email: 'a@b.com' } }),
  prisma.post.create({ data: { title: 'Hello', authorId: 1 } }),
]);

// Or interactive:
await prisma.$transaction(async (tx) => {
  const u = await tx.user.create({ data: { email: 'a@b.com' } });
  await tx.post.create({ data: { title: 'Hi', authorId: u.id } });
});

// Pagination (cursor)
const page = await prisma.user.findMany({
  take: 20,
  cursor: { id: lastId },
  skip: 1,
});
```

### Type safety
Prisma generates TS types from schema. Full end-to-end type safety.

### Indexes
```prisma
model User {
  id    Int    @id @default(autoincrement())
  email String @unique
  name  String

  @@index([name])
  @@unique([email, name])
}
```

### Raw SQL (escape hatch)
```ts
const users = await prisma.$queryRaw`SELECT * FROM users WHERE email = ${email}`;
```

### Performance
- Connection pool: configure in `DATABASE_URL` (`?connection_limit=10`).
- Use `select` to fetch only needed fields.
- Watch for N+1 with nested reads.
- Use `findMany` with `include` for relations.
- Avoid `findMany` without `take` (could load huge data).

### Prisma vs Drizzle
→ [ORM/README.md#prisma-vs-drizzle](../ORM/README.md)

Prisma: better DX, generated client, schema language. Heavier.
Drizzle: SQL-like, lighter, edge-friendly, more control.

For new TS apps: either works. Pick by preference.

## Common Mistakes

- ❌ Forgetting `prisma generate` after schema change.
- ❌ N+1 (use `include` or `select`).
- ❌ No transactions.
- ❌ `findMany` without limit.
- ❌ Not using `select` (over-fetching).

## Tools

- Prisma docs: https://www.prisma.io/docs
- Prisma Studio: built-in GUI.
- Prisma Migrate: built-in.
- Prisma Accelerate: edge cache (paid).
- Prisma Pulse: real-time (paid).

## References

- Prisma: https://www.prisma.io/

## Exercises

1. Build a CRUD app with Prisma + Postgres.
2. Add relations + transactions.
3. Set up migrations in CI.

## Projects

- Build a multi-tenant SaaS with Prisma + Postgres + row-level security.

---

**Previous:** [SQLite/](../SQLite/) · **Next:** [Drizzle/](../Drizzle/) · **Related:** [ORM/](../ORM/)
