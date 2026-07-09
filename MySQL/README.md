# MySQL

> MySQL: ubiquitous relational DB. Powers WordPress, Facebook, and countless apps.

---

## Purpose

Use MySQL/MariaDB for relational workloads.

## Prerequisites

- SQL basics, [Databases/](../Databases/).

## Learning Outcome

You can build, query, and optimize a MySQL database.

## Dependencies

- MySQL 8+ or MariaDB 11+.

## Related Files

- [Databases/](../Databases/) · [PostgreSQL/](../PostgreSQL/) · [SQLite/](../SQLite/)

## AI Instructions

When using MySQL:
1. Use MySQL 8+ (or MariaDB 11+).
2. Use InnoDB engine (default).
3. Use `BIGINT AUTO_INCREMENT` or UUID for PKs.
4. Index FKs and frequent WHERE columns.
5. Use `DATETIME` or `TIMESTAMP` (note: TIMESTAMP is UTC, auto-converts).
6. Use `DECIMAL` for money.
7. Use `EXPLAIN` to optimize.
8. Use connection pooling (ProxySQL).

## Human Notes

### MySQL vs Postgres
- MySQL: simpler, faster for simple CRUD, huge ecosystem (WordPress).
- Postgres: more features, JSONB, extensions, stricter.

For new apps without specific MySQL needs, prefer Postgres.

### Engines
- **InnoDB** (default) — ACID, transactions, row-level locking.
- **MyISAM** — old, no transactions, table-level locking. Avoid.
- **MEMORY** — in-memory, volatile.

### Schema
```sql
CREATE TABLE users (
  id BIGINT AUTO_INCREMENT PRIMARY KEY,
  email VARCHAR(255) NOT NULL UNIQUE,
  name VARCHAR(100) NOT NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  INDEX idx_email (email)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

### Important settings
- `utf8mb4` charset (not `utf8` — it's 3-byte and breaks emoji).
- `utf8mb4_unicode_ci` collation.
- `innodb_buffer_pool_size` = 50-75% of RAM.
- `innodb_log_file_size` based on write volume.

### JSON
MySQL 8 has JSON type:
```sql
INSERT INTO users (email, prefs) VALUES ('a@b.com', '{"theme":"dark"}');
SELECT prefs->>'$.theme' FROM users;
```
Less powerful than Postgres JSONB.

### Full-text
```sql
CREATE FULLTEXT INDEX idx_posts_ft ON posts (title, body);
SELECT * FROM posts WHERE MATCH(title, body) AGAINST ('postgres' IN NATURAL LANGUAGE MODE);
```

### Replication
- Async by default.
- Read replicas for read scale.
- Group replication / InnoDB Cluster for HA.

### Performance
- `EXPLAIN`.
- `slow_query_log`.
- `performance_schema`.
- ProxySQL for pooling.

### When to use MySQL
- Existing MySQL ecosystem.
- WordPress / Magento.
- Team familiarity.
- Simple CRUD at scale.

### When NOT
- Need rich JSON (Postgres better).
- Need extensions (PostGIS, pgvector — Postgres).
- New app without MySQL bias.

## Common Mistakes

- ❌ `utf8` instead of `utf8mb4`.
- ❌ MyISAM engine.
- ❌ No indexes on FKs.
- ❌ Money as float.
- ❌ TIMESTAMP confusion (auto UTC).
- ❌ No backups.

## Tools

- MySQL docs: https://dev.mysql.com/doc/
- MariaDB docs: https://mariadb.com/kb/en/documentation/
- ProxySQL: https://proxysql.com/
- PlanetScale: serverless MySQL (Vitess).

## Further Reading

- *High Performance MySQL* — Silvia Botros et al.

## Exercises

1. Build a CRUD app with MySQL.
2. Add full-text search.
3. Set up read replication.

## Projects

- Build a WordPress-style blog DB.

---

**Previous:** [PostgreSQL/](../PostgreSQL/) · **Next:** [MongoDB/](../MongoDB/) · **Related:** [Databases/](../Databases/)
