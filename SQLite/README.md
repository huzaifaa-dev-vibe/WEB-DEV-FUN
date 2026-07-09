# SQLite

> Embedded SQL database. No server. Just a file. Used everywhere.

---

## Purpose

Use SQLite for local-first apps, prototypes, edge databases.

## Prerequisites

- SQL basics, [Databases/](../Databases/).

## Learning Outcome

You can use SQLite effectively for apps that don't need a server DB.

## Dependencies

- SQLite (built into most languages).

## Related Files

- [Databases/](../Databases/) · [PostgreSQL/](../PostgreSQL/) · [Prisma/](../Prisma/) · [Drizzle/](../Drizzle/)

## AI Instructions

When using SQLite:
1. Enable WAL mode for concurrent reads.
2. Use prepared statements (prevent SQL injection).
3. Set `busy_timeout` for write contention.
4. Use `STRICT` tables (typed).
5. Great for: local-first apps, prototypes, edge, embedded, tests.

## Human Notes

### When to use SQLite
- Local-first apps (desktop, mobile).
- Prototypes.
- Edge / serverless (Cloudflare D1, Turso).
- Tests (replace Postgres for fast tests).
- Single-instance small web app.
- Embedded in apps.

### When NOT to use
- Many concurrent writers.
- Multiple app servers (no network protocol).
- Need rich user management.

### Modern SQLite (libSQL, Turso)
- libSQL: open-source SQLite fork with replication.
- Turso: serverless libSQL at the edge.
- Cloudflare D1: serverless SQLite.

### Hello
```sql
-- CLI
sqlite3 myapp.db
CREATE TABLE users (id INTEGER PRIMARY KEY, name TEXT NOT NULL);
INSERT INTO users (name) VALUES ('Alice');
SELECT * FROM users;
```

### WAL mode
```sql
PRAGMA journal_mode=WAL;
PRAGMA synchronous=NORMAL;
PRAGMA busy_timeout=5000;
```
- WAL allows concurrent reads while writing.
- Single writer at a time.

### Strict tables (3.37+)
```sql
CREATE TABLE users (
  id INTEGER PRIMARY KEY,
  name TEXT NOT NULL,
  age INTEGER NOT NULL CHECK (age >= 0)
) STRICT;
```
Strict type enforcement (otherwise SQLite is permissive).

### JSON (3.38+)
```sql
CREATE TABLE events (id INTEGER PRIMARY KEY, data JSON);
INSERT INTO events (data) VALUES ('{"type":"signup","user":"alice"}');
SELECT data->>'$.user' FROM events WHERE data->>'$.type' = 'signup';
```

### FTS (Full-Text Search)
```sql
CREATE VIRTUAL TABLE posts_fts USING fts5(title, body);
INSERT INTO posts_fts (title, body) VALUES ('Hello', 'World');
SELECT * FROM posts_fts WHERE posts_fts MATCH 'hello';
```

### Performance
- Very fast for reads.
- Writes are serialized.
- Use indexes like any RDBMS.
- `PRAGMA optimize` periodically.

### Backups
- Stop writes, copy file.
- Or: `sqlite3 myapp.db ".backup backup.db"`.

### Limitations
- Single writer.
- No built-in replication (use libSQL / Turso).
- 281 TB max DB size (theoretical).

## Common Mistakes

- ❌ No WAL mode (slow for concurrent access).
- ❌ No `busy_timeout` (write contention errors).
- ❌ Treating as truly server-grade (it's not for multi-instance).
- ❌ Not using prepared statements.

## Tools

- SQLite docs: https://www.sqlite.org/docs.html
- SQLite Studio: https://github.com/frectonz/sqlite-studio
- DB Browser for SQLite: https://sqlitebrowser.org/
- Turso: https://turso.tech/
- Cloudflare D1: https://developers.cloudflare.com/d1/
- libSQL: https://github.com/tursodatabase/libsql

## Further Reading

- SQLite docs: https://www.sqlite.org/
- "SQLite is not a toy database": https://www.sqlite.org/whentouse.html

## Exercises

1. Build a local-first app with SQLite.
2. Enable WAL + FTS.
3. Deploy to Turso or Cloudflare D1.

## Projects

- Build a serverless app with Cloudflare D1.
- Build a desktop app with SQLite (Electron / Tauri).

---

**Previous:** [Redis/](../Redis/) · **Next:** [Prisma/](../Prisma/) · **Related:** [Databases/](../Databases/)
