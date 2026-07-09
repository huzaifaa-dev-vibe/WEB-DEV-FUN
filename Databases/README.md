# Databases

> Where data lives. Pick the right one. Schema matters.

---

## Purpose

Master database concepts: relational, document, cache, vector, time-series.

## Prerequisites

- [Backend/](../Backend/), basic SQL.

## Learning Outcome

You can pick the right database, model data, write efficient queries.

## Dependencies

- None (conceptual).

## Related Files

- [PostgreSQL/](../PostgreSQL/) · [MySQL/](../MySQL/) · [MongoDB/](../MongoDB/) · [Redis/](../Redis/) · [SQLite/](../SQLite/) · [Prisma/](../Prisma/) · [Drizzle/](../Drizzle/) · [ORM/](../ORM/)

## Decision Tree

```
What's the data shape?
├─ Relational (users, orders, products) → PostgreSQL (default)
├─ Document (varied, nested) → MongoDB (or Postgres JSONB)
├─ Key-value cache → Redis
├─ Embedded (no server) → SQLite
├─ Time-series → TimescaleDB (Postgres extension) or ClickHouse
├─ Search → Postgres FTS → Meilisearch → Elasticsearch at scale
├─ Vector (AI) → pgvector (Postgres) → Qdrant → Pinecone
├─ Graph → Neo4j (or Postgres with recursive CTEs)
└─ Wide-column → Cassandra / ScyllaDB (rare in startups)
```

## Human Notes

### Default stack
- **Postgres** for relational.
- **Redis** for cache / queue.
- **S3/R2** for files.
- That covers 90% of apps.

### ACID
- Atomicity — all or nothing.
- Consistency — valid state.
- Isolation — concurrent txns don't interfere.
- Durability — committed = permanent.

### CAP theorem
- Consistency.
- Availability.
- Partition tolerance.

Pick 2. In distributed systems, you get CP or AP.

### BASE (opposite of ACID)
- Basically Available.
- Soft state.
- Eventual consistency.

### Normalization
- 1NF: atomic values.
- 2NF: no partial deps on composite keys.
- 3NF: no transitive deps.
- BCNF: stricter 3NF.

In practice, denormalize for read performance, normalize for write integrity.

### Indexes
- B-tree (default) — equality + range.
- Hash — equality only.
- GIN — full-text, arrays, JSONB.
- GiST — geometric, range.
- BRIN — large tables, ordered.

Don't index everything — slows writes.

### Query optimization
- `EXPLAIN ANALYZE`.
- Avoid `SELECT *`.
- Watch for N+1.
- Add indexes for frequent WHERE / ORDER BY.
- Use pagination (cursor > offset).
- Use connection pooling (PgBouncer).

### Migrations
- Forward-only in prod.
- Expand → migrate → contract pattern.
- Always test on prod-sized data.

### Replication
- Read replicas for read scale.
- Streaming replication for HA.
- Logical replication for selective sync.

### Sharding
- Horizontal scaling.
- Last resort — try vertical scaling first.

### Caching
- Cache-aside: app reads cache, then DB on miss.
- Write-through: write to cache + DB.
- Write-behind: write to cache, async to DB.

### Vector DBs (for AI)
- pgvector (Postgres extension) — start here.
- Qdrant, Weaviate, Chroma, Pinecone — at scale.
- LanceDB — embedded.

### When to use what
| Need | Use |
|---|---|
| Relational data, transactions | Postgres |
| Document data, schema varies | MongoDB or Postgres JSONB |
| Cache, sessions, rate limit | Redis |
| Embedded (no server) | SQLite |
| Time-series at scale | TimescaleDB, ClickHouse |
| Full-text search | Postgres FTS → Meilisearch → Elasticsearch |
| Vector search (AI) | pgvector → Qdrant → Pinecone |
| Graph (relationships) | Neo4j |
| Wide-column (massive scale) | Cassandra |
| Analytics (OLAP) | ClickHouse, DuckDB, BigQuery |

## Common Mistakes

- ❌ Wrong DB for the job (e.g., Mongo for relational).
- ❌ No indexes on FKs.
- ❌ N+1 queries.
- ❌ No migrations.
- ❌ Money as float.
- ❌ No transactions.
- ❌ Storing files in DB.
- ❌ No backups.
- ❌ No connection pooling.
- ❌ UUID v4 for clustered PKs.

## Tools

- TablePlus, DBeaver, pgAdmin — GUIs.
- Postgres.ai — DB lab.
- Atlas — declarative migrations.

## References

- Use The Index, Luke: https://use-the-index-luke.com/
- PostgreSQL docs: https://www.postgresql.org/docs/
- MongoDB docs: https://www.mongodb.com/docs/
- Redis docs: https://redis.io/docs/
- Designing Data-Intensive Applications (book).

## Further Reading

- *Designing Data-Intensive Applications* — Martin Kleppmann
- *Database Internals* — Alex Petrov
- *SQL Antipatterns* — Bill Karwin

## Exercises

1. Model a blog with users, posts, comments, tags.
2. Add indexes. Verify with EXPLAIN.
3. Migrate to add a column without downtime.

## Projects

- Build a multi-tenant SaaS database schema (row-level security).

---

**Previous:** [.NET/](../.NET/) · **Next:** [PostgreSQL/](../PostgreSQL/) · **Related:** [ORM/](../ORM/)
