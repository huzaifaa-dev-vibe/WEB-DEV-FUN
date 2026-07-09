# ORM

> Object-Relational Mapping. Bridges objects and tables. Use wisely.

---

## Purpose

Understand ORM patterns, when to use them, when to use raw SQL.

## Prerequisites

- [Databases/](../Databases/), [PostgreSQL/](../PostgreSQL/).

## Learning Outcome

You can pick the right ORM/SQL approach for your app.

## Dependencies

- A database.

## Related Files

- [Prisma/](../Prisma/) · [Drizzle/](../Drizzle/) · [PostgreSQL/](../PostgreSQL/) · [ORM/n-plus-1.md](n-plus-1.md)

## AI Instructions

When picking ORM:
1. **TS/JS app**: Prisma or Drizzle.
2. **Python**: SQLAlchemy or SQLModel.
3. **Go**: GORM or sqlc.
4. **Rust**: sqlx or diesel.
5. **Java**: Hibernate / JPA.
6. **.NET**: EF Core.
7. **Ruby**: Active Record.
8. **PHP**: Eloquent (Laravel) or Doctrine (Symfony).
9. Use raw SQL when ORM gets in the way (complex queries, perf-critical).

## Human Notes

### ORM trade-offs

**Pros:**
- Type safety (in typed languages).
- Less boilerplate.
- Migrations tooling.
- Relations handled.
- Multi-DB support sometimes.

**Cons:**
- Performance overhead.
- N+1 problem.
- "ORM impedance mismatch."
- Hard to express complex SQL.
- Vendor lock-in.

### The N+1 problem
```js
// BAD: 1 query for users, then 1 query per user for posts
const users = await User.findMany();
for (const u of users) {
  console.log(await u.posts); // 1 query each!
}
// Total: 1 + N queries

// GOOD: 2 queries with eager loading
const users = await User.findMany({ include: { posts: true } });
// Total: 2 queries
```

→ [ORM/n-plus-1.md](n-plus-1.md)

### Patterns

#### Active Record
- Model has `save()`, `delete()`, static finders.
- e.g., Rails Active Record, Laravel Eloquent.
- Simple, but couples model to DB.

#### Data Mapper
- Repository pattern. Models are plain.
- e.g., Doctrine, TypeORM (sort of).
- More flexible, more code.

#### Query Builder
- Programmatic SQL construction.
- e.g., Knex, Kysely.
- SQL-like, type-safe.

#### Row Mapper
- Map SQL results to objects manually.
- e.g., sqlx (Go/Rust).
- Full control, more code.

### Prisma vs Drizzle

| | Prisma | Drizzle |
|---|---|---|
| Schema | Prisma DSL | TypeScript |
| Client | Generated | Inferred |
| Edge | Limited | Yes |
| Bundle | Larger | Smaller |
| DX | Excellent | Good |
| SQL-likeness | Abstract | Very close |
| Migrations | Excellent | Good |
| Studio | Yes | Yes |
| Learning curve | Low | Medium |

For most TS apps: either works.
For edge / lightweight: Drizzle.
For max DX / new to ORMs: Prisma.

### When to use raw SQL
- Complex analytical queries.
- Performance-critical paths.
- Bulk operations (`INSERT ... ON CONFLICT`, `COPY`).
- DB-specific features (CTEs, window functions).
- Migration scripts.

### When to use ORM
- CRUD-heavy apps.
- Type safety matters.
- Multi-table relations.
- Migrations needed.
- Team wants abstraction.

### Hybrid approach
Use ORM for 80%, raw SQL for 20%. Most ORMs support escape hatches.

## Common Mistakes

- ❌ N+1 queries.
- ❌ Trusting ORM-generated SQL blindly.
- ❌ Using ORM for analytics.
- ❌ No transactions.
- ❌ Over-fetching (no `select`).
- ❌ Not using indexes (ORM doesn't auto-create).

## Tools

- See specific language folders.

## References

- P of EAA (Martin Fowler): https://martinfowler.com/eaaCatalog/
- "ORM is an anti-pattern": https://www.yegor256.com/2014/12/01/orm-offensive-anti-pattern.html (debate)

## Further Reading

- *Patterns of Enterprise Application Architecture* — Martin Fowler

## Exercises

1. Implement N+1 in a sample app. Fix with eager loading.
2. Convert an ORM query to raw SQL for perf.
3. Compare Prisma vs Drizzle on the same schema.

## Projects

- Build a multi-tenant SaaS with ORM + row-level security.

---

**Previous:** [Drizzle/](../Drizzle/) · **Next:** [Deployment/](../Deployment/) · **Related:** [Databases/](../Databases/)
