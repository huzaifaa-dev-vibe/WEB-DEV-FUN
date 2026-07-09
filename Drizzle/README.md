# Drizzle

> SQL-like TypeScript ORM. Lightweight, edge-friendly, full control.

---

## Purpose

Use Drizzle for type-safe SQL in TS apps, especially on the edge.

## Prerequisites

- [TypeScript/](../TypeScript/), SQL, [PostgreSQL/](../PostgreSQL/).

## Learning Outcome

You can use Drizzle for schema, migrations, queries.

## Dependencies

- Node.js / Bun / Deno / edge runtime.

## Related Files

- [Prisma/](../Prisma/) · [ORM/](../ORM/) · [PostgreSQL/](../PostgreSQL/) · [Databases/](../Databases/)

## AI Instructions

When using Drizzle:
1. Use Drizzle 0.30+.
2. Define schema in TS.
3. Use `drizzle-kit` for migrations.
4. Use the SQL-like query API.
5. Works on edge (Cloudflare Workers, Vercel Edge).
6. Use transactions.
7. Use `prepared()` for prepared statements.

## Human Notes

### Why Drizzle over Prisma
- Lighter (no generated client).
- SQL-like API (closer to SQL).
- Edge-friendly (no Rust binary).
- More control.
- Free / open-source only.

### Why Prisma over Drizzle
- Better DX (schema language, Studio GUI).
- Auto-generated types.
- Larger community.
- Maturity.

### Schema
```ts
// schema.ts
import { pgTable, serial, text, timestamp, integer, boolean } from 'drizzle-orm/pg-core';

export const users = pgTable('users', {
  id: serial('id').primaryKey(),
  email: text('email').notNull().unique(),
  name: text('name'),
  active: boolean('active').default(true),
  createdAt: timestamp('created_at').defaultNow(),
});

export const posts = pgTable('posts', {
  id: serial('id').primaryKey(),
  title: text('title').notNull(),
  body: text('body').notNull(),
  authorId: integer('author_id').notNull().references(() => users.id),
  createdAt: timestamp('created_at').defaultNow(),
});
```

### Client
```ts
import { drizzle } from 'drizzle-orm/postgres-js';
import postgres from 'postgres';
import * as schema from './schema';

const client = postgres(process.env.DATABASE_URL!);
export const db = drizzle(client, { schema });
```

### Queries
```ts
import { eq, and, desc, like } from 'drizzle-orm';

// Create
const [user] = await db.insert(users).values({ email: 'a@b.com' }).returning();

// Read
const user = await db.query.users.findFirst({ where: eq(users.id, 1) });
const all = await db.select().from(users).where(eq(users.active, true));

// Update
await db.update(users).set({ name: 'Bob' }).where(eq(users.id, 1));

// Delete
await db.delete(users).where(eq(users.id, 1));

// Joins
const usersWithPosts = await db
  .select()
  .from(users)
  .leftJoin(posts, eq(users.id, posts.authorId));

// Relations API (similar to Prisma)
const userWithPosts = await db.query.users.findFirst({
  with: { posts: true },
});

// Pagination (cursor)
const page = await db.query.users.findMany({
  limit: 20,
  where: gt(users.id, lastId),
  orderBy: users.id,
});

// Transactions
await db.transaction(async (tx) => {
  await tx.insert(users).values({ email: 'a@b.com' });
  await tx.insert(posts).values({ title: 'Hi', authorId: 1 });
});

// Prepared
const getUser = db.select().from(users).where(eq(users.id, ?)).prepare();
const u = await getUser.execute(1);
```

### Migrations
```bash
npx drizzle-kit generate  # generate SQL from schema
npx drizzle-kit migrate   # apply
npx drizzle-kit studio    # GUI
```

### Edge runtime
Drizzle works on:
- Cloudflare Workers (D1, Hyperdrive).
- Vercel Edge (Neon, PlanetScale).
- Bun, Deno.

Prisma struggles on edge (Rust binary).

### Type safety
Full type inference from schema. No codegen step.

## Common Mistakes

- ❌ Not running migrations.
- ❌ Forgetting `.returning()` on inserts.
- ❌ N+1 with relations (use `with`).
- ❌ Raw SQL without parameters.

## Tools

- Drizzle docs: https://orm.drizzle.team/
- Drizzle Studio: built-in GUI.
- Drizzle Kit: migrations.

## References

- Drizzle: https://orm.drizzle.team/

## Exercises

1. Build a CRUD app with Drizzle + Postgres.
2. Deploy to Cloudflare Workers with D1.
3. Compare to Prisma in same app.

## Projects

- Build an edge app with Drizzle + Neon (serverless Postgres).

---

**Previous:** [Prisma/](../Prisma/) · **Next:** [ORM/](../ORM/) · **Related:** [PostgreSQL/](../PostgreSQL/)
