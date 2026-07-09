# PostgreSQL

> The world's most advanced open-source relational database. Default for 90% of apps.

---

## Purpose

Master Postgres: schema, queries, indexes, JSONB, full-text search, performance.

## Prerequisites

- SQL basics, [Databases/](../Databases/).

## Learning Outcome

You can design, query, and optimize Postgres for production.

## Dependencies

- Postgres 16+.

## Related Files

- [Databases/](../Databases/) · [MySQL/](../MySQL/) · [SQLite/](../SQLite/) · [Prisma/](../Prisma/) · [Drizzle/](../Drizzle/) · [PostgreSQL/migrations.md](migrations.md) · [PostgreSQL/indexes.md](indexes.md) · [PostgreSQL/jsonb.md](jsonb.md)

## AI Instructions

When using Postgres:
1. Use Postgres 16+ (or 17+).
2. Use `BIGSERIAL` or UUID v7 for PKs.
3. Index FKs and frequent WHERE columns.
4. Use `JSONB` for semi-structured data (with indexes).
5. Use `TIMESTAMPTZ` for timestamps.
6. Use `DECIMAL` / `NUMERIC` for money.
7. Use `pgvector` for AI/embeddings.
8. Use `EXPLAIN ANALYZE` to optimize.
9. Use connection pooling (PgBouncer).
10. Backup regularly. Test restores.

## Human Notes

### Why Postgres
- ACID.
- SQL standard.
- JSONB (best of both worlds).
- Rich extension ecosystem (pgvector, PostGIS, TimescaleDB, etc.).
- MVCC (multi-version concurrency control).
- Free and open-source.
- 30+ years of development.

### Data types
- `INTEGER`, `BIGINT`, `NUMERIC`, `REAL`, `DOUBLE PRECISION`.
- `TEXT`, `VARCHAR(n)`, `CHAR(n)`.
- `BOOLEAN`.
- `DATE`, `TIME`, `TIMESTAMP`, `TIMESTAMPTZ`, `INTERVAL`.
- `UUID`, `JSONB`, `JSON`, `ARRAY`.
- `BYTEA` (binary).
- `INET`, `CIDR` (IP).
- Custom types: `CREATE TYPE`.

### Schema design
```sql
CREATE TABLE users (
  id BIGSERIAL PRIMARY KEY,
  email TEXT NOT NULL UNIQUE,
  name TEXT NOT NULL,
  preferences JSONB NOT NULL DEFAULT '{}',
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

CREATE TABLE posts (
  id BIGSERIAL PRIMARY KEY,
  user_id BIGINT NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  title TEXT NOT NULL,
  body TEXT NOT NULL,
  published_at TIMESTAMPTZ,
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

CREATE INDEX idx_posts_user_id ON posts(user_id);
CREATE INDEX idx_posts_published ON posts(published_at DESC) WHERE published_at IS NOT NULL;
```

### Indexes
- B-tree (default).
- `CREATE INDEX ... USING hash`.
- `CREATE INDEX ... USING gin` (JSONB, FTS, arrays).
- `CREATE INDEX ... USING gist` (geometric).
- Partial: `CREATE INDEX ... WHERE condition`.
- Unique: `CREATE UNIQUE INDEX ...`.
- Expression: `CREATE INDEX ... ON tbl (lower(email))`.

→ [PostgreSQL/indexes.md](indexes.md)

### JSONB
```sql
INSERT INTO users (email, preferences) VALUES ('a@b.com', '{"theme": "dark", "lang": "en"}');

SELECT * FROM users WHERE preferences @> '{"theme": "dark"}';
SELECT preferences->>'theme' FROM users;
UPDATE users SET preferences = jsonb_set(preferences, '{theme}', '"light"');

CREATE INDEX idx_users_prefs ON users USING gin (preferences);
```

→ [PostgreSQL/jsonb.md](jsonb.md)

### Full-text search
```sql
CREATE INDEX idx_posts_fts ON posts USING gin (to_tsvector('english', title || ' ' || body));

SELECT * FROM posts
WHERE to_tsvector('english', title || ' ' || body) @@ to_tsquery('postgres & tutorial')
ORDER BY ts_rank(...) DESC;
```

Good for medium scale. Switch to Meilisearch/Typesense at scale.

### Transactions
```sql
BEGIN;
INSERT INTO accounts (id, balance) VALUES (1, 100);
UPDATE accounts SET balance = balance - 50 WHERE id = 1;
COMMIT;  -- or ROLLBACK;
```

### Common Table Expressions (CTEs)
```sql
WITH active_users AS (
  SELECT * FROM users WHERE active = true
)
SELECT * FROM active_users WHERE created_at > '2024-01-01';
```

Recursive CTEs for trees/graphs.

### Window functions
```sql
SELECT
  user_id,
  created_at,
  ROW_NUMBER() OVER (PARTITION BY user_id ORDER BY created_at DESC) as rn
FROM posts;
```

### EXPLAIN ANALYZE
```sql
EXPLAIN ANALYZE SELECT * FROM users WHERE email = 'a@b.com';
```
- Seq Scan = bad (no index used).
- Index Scan = good.
- Index Only Scan = best.

→ [PostgreSQL/explain.md](explain.md)

### Migrations
- Forward-only in prod.
- Expand → migrate → contract pattern.
- Use Prisma Migrate, Drizzle Kit, node-pg-migrate, or Atlas.

→ [PostgreSQL/migrations.md](migrations.md)

### Connection pooling
- Postgres forks a process per connection.
- Use PgBouncer for pooling (transaction mode).
- App-level pool: max 10-25 conns per instance.

### Replication
- Streaming (physical).
- Logical (selective, cross-version).
- Read replicas for read scale.

### Backups
- `pg_dump` for logical.
- WAL archiving + `pgBackRest` for PITR.
- Test restores regularly!

### Extensions
- `pgvector` — vector search (AI).
- `PostGIS` — geospatial.
- `TimescaleDB` — time-series.
- `pg_stat_statements` — query stats.
- `pg_trgm` — trigram similarity.
- `uuid-ossp` / `pgcrypto` — UUIDs.

### Performance tuning
- `shared_buffers` — 25% of RAM.
- `effective_cache_size` — 50-75% of RAM.
- `work_mem` — sort/hash memory.
- `maintenance_work_mem` — VACUUM/CREATE INDEX memory.
- `max_connections` — keep low, use PgBouncer.

### Common mistakes
- ❌ `SELECT *`.
- ❌ No indexes on FKs.
- ❌ UUID v4 for clustered PKs (fragmentation).
- ❌ Money as float.
- ❌ `TIMESTAMP` without TZ.
- ❌ Storing files as BYTEA.
- ❌ No VACUUM/ANALYZE maintenance.
- ❌ Too many connections.

## Tools

- Postgres docs: https://www.postgresql.org/docs/
- Postgres Wiki: https://wiki.postgresql.org/
- pgAdmin: https://www.pgadmin.org/
- TablePlus / DBeaver: GUIs.
- Postgres.ai: DB lab.
- pgvector: https://github.com/pgvector/pgvector
- PostGIS: https://postgis.net/

## Further Reading

- *The Art of PostgreSQL* — Dimitri Fontaine
- *PostgreSQL Up and Running* — Regina Obe & Leo Hsu
- Use The Index, Luke: https://use-the-index-luke.com/

## Exercises

1. Design a multi-tenant schema (with row-level security).
2. Add JSONB column + GIN index.
3. Write a recursive CTE for a comment tree.
4. Optimize a slow query with EXPLAIN ANALYZE.

## Projects

- Build a Postgres-backed analytics dashboard.
- Build a RAG app with pgvector.

---

**Previous:** [Databases/](../Databases/) · **Next:** [MySQL/](../MySQL/) · **Related:** [Prisma/](../Prisma/)
