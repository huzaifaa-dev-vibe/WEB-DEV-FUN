# CHEATSHEET

> Quick syntax for everything. `Ctrl/Cmd+F` to jump.

---

## HTML

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Page description">
  <title>Title</title>
  <link rel="icon" href="/favicon.ico">
  <link rel="stylesheet" href="/styles.css">
</head>
<body>
  <header><nav>...</nav></header>
  <main>
    <article>
      <h1>Heading</h1>
      <p>Paragraph</p>
      <ul><li>Item</li></ul>
      <ol><li>Item</li></ol>
      <a href="..." rel="noopener noreferrer" target="_blank">Link</a>
      <img src="..." alt="..." width="..." height="..." loading="lazy">
      <figure><img src="..." alt="..."><figcaption>Caption</figcaption></figure>
      <blockquote cite="...">Quote</blockquote>
      <code>inline code</code>
      <pre><code>block code</code></pre>
      <details><summary>Summary</summary>Details</details>
    </article>
    <form action="/submit" method="POST">
      <label for="name">Name</label>
      <input id="name" name="name" type="text" required>
      <input type="email" name="email" required>
      <input type="checkbox" name="agree" required>
      <select name="role"><option value="user">User</option></select>
      <textarea name="bio"></textarea>
      <button type="submit">Submit</button>
    </form>
  </main>
  <footer>...</footer>
</body>
</html>
```

---

## CSS

### Layout
```css
/* Flexbox */
.flex { display: flex; gap: 1rem; }
.flex-center { display: flex; align-items: center; justify-content: center; }
.flex-between { display: flex; justify-content: space-between; }
.flex-col { display: flex; flex-direction: column; }

/* Grid */
.grid { display: grid; gap: 1rem; grid-template-columns: repeat(3, 1fr); }
.grid-auto { grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); }
.grid-span { grid-column: span 2; }

/* Center anything */
.center { display: grid; place-items: center; }

/* Sticky header */
.sticky { position: sticky; top: 0; z-index: 10; }
```

### Units
```css
/* Dynamic viewport (mobile-safe) */
.full-screen { height: 100dvh; }
/* Static */
.static-h { height: 100vh; }
/* Responsive type */
h1 { font-size: clamp(2rem, 5vw, 4rem); }
```

### Variables / Tokens
```css
:root {
  --color-bg: #ffffff;
  --color-fg: #0a0a0a;
  --color-accent: oklch(0.6 0.2 250);
  --space-1: 0.25rem;  /* 4px */
  --space-2: 0.5rem;   /* 8px */
  --space-3: 0.75rem;  /* 12px */
  --space-4: 1rem;     /* 16px */
  --space-6: 1.5rem;   /* 24px */
  --space-8: 2rem;     /* 32px */
  --radius: 8px;
  --shadow: 0 1px 3px rgb(0 0 0 / 0.1);
}

.dark {
  --color-bg: #0a0a0a;
  --color-fg: #fafafa;
}

@media (prefers-color-scheme: dark) {
  :root { --color-bg: #0a0a0a; --color-fg: #fafafa; }
}
```

### Animations
```css
.fade-in { animation: fadeIn 0.3s ease-out; }
@keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after { animation-duration: 0.01ms !important; transition-duration: 0.01ms !important; }
}
```

### Container Queries
```css
.card-container { container-type: inline-size; }
@container (min-width: 400px) {
  .card { grid-template-columns: 1fr 2fr; }
}
```

### Pseudo-classes
```css
:hover { }
:focus-visible { outline: 2px solid var(--color-accent); }
:active { }
:disabled { opacity: 0.5; }
:first-child { }
:last-child { }
:nth-child(odd) { }
:has(+ img) { } /* parent has */
:not(.active) { }
```

---

## JavaScript

### Modern syntax
```js
// Destructuring
const { name, age = 18, ...rest } = user;
const [first, ...others] = arr;

// Spread
const merged = { ...a, ...b };
const arr2 = [...arr, newItem];

// Optional chaining + nullish coalescing
const city = user?.address?.city ?? 'Unknown';

// Template literals
const greeting = `Hello, ${name}!`;

// Arrow functions
const add = (a, b) => a + b;
const log = msg => console.log(msg);

// Async/await
async function fetchUser(id) {
  try {
    const res = await fetch(`/api/users/${id}`);
    if (!res.ok) throw new Error(`HTTP ${res.status}`);
    return await res.json();
  } catch (err) {
    console.error('[fetchUser]', err);
    throw err;
  }
}
```

### Common patterns
```js
// Debounce
const debounce = (fn, ms) => {
  let t;
  return (...args) => {
    clearTimeout(t);
    t = setTimeout(() => fn(...args), ms);
  };
};

// Throttle
const throttle = (fn, ms) => {
  let last = 0;
  return (...args) => {
    const now = Date.now();
    if (now - last >= ms) { last = now; fn(...args); }
  };
};

// Map/Filter/Reduce
const squares = nums.map(n => n * n);
const evens = nums.filter(n => n % 2 === 0);
const sum = nums.reduce((acc, n) => acc + n, 0);

// Group by
const byRole = users.reduce((acc, u) => {
  (acc[u.role] ||= []).push(u);
  return acc;
}, {});

// Unique
const unique = [...new Set(arr)];

// Sleep
const sleep = ms => new Promise(r => setTimeout(r, ms));
```

### Fetch
```js
// GET
const res = await fetch('/api/data');
const data = await res.json();

// POST JSON
const res = await fetch('/api/data', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ name: 'Alice' }),
});

// FormData
const fd = new FormData(form);
await fetch('/upload', { method: 'POST', body: fd });

// Abort
const ctrl = new AbortController();
setTimeout(() => ctrl.abort(), 5000);
await fetch('/api', { signal: ctrl.signal });
```

### LocalStorage / SessionStorage / IndexedDB
```js
localStorage.setItem('key', JSON.stringify(value));
const value = JSON.parse(localStorage.getItem('key'));
localStorage.removeItem('key');
```

---

## TypeScript

```typescript
// Basic types
let str: string = 'hello';
let num: number = 42;
let bool: boolean = true;
let arr: number[] = [1, 2, 3];
let tuple: [string, number] = ['a', 1];
let nothing: null = null;
let unknown: unknown = 'maybe';

// Interfaces & Types
interface User { id: string; name: string; age?: number; readonly role: string; }
type Status = 'active' | 'inactive' | 'banned';
type Result<T> = { ok: true; value: T } | { ok: false; error: string };

// Generics
function first<T>(arr: T[]): T | undefined { return arr[0]; }

// Utility types
type PartialUser = Partial<User>;
type RequiredUser = Required<User>;
type ReadonlyUser = Readonly<User>;
type PickUser = Pick<User, 'id' | 'name'>;
type OmitUser = Omit<User, 'age'>;
type RecordUsers = Record<string, User>;
type ReturnTypeOf<T> = T extends (...args: any[]) => infer R ? R : never;
type AwaitedType<T> = Awaited<T>;

// Type narrowing
function handle(x: string | number) {
  if (typeof x === 'string') return x.toUpperCase();
  return x.toFixed(2);
}

// `unknown` over `any`
function parse(s: string): unknown { return JSON.parse(s); }
```

---

## React (Hooks)

```jsx
import { useState, useEffect, useMemo, useCallback, useRef, useReducer, useContext } from 'react';

// State
const [count, setCount] = useState(0);
const [form, setForm] = useState({ name: '', email: '' });

// Effect
useEffect(() => {
  const handler = () => console.log('resize');
  window.addEventListener('resize', handler);
  return () => window.removeEventListener('resize', handler);
}, []);

// Memo
const expensive = useMemo(() => compute(data), [data]);

// Callback
const handleClick = useCallback(() => { /* ... */ }, [dep]);

// Ref
const inputRef = useRef(null);
useEffect(() => inputRef.current?.focus(), []);

// Reducer
const [state, dispatch] = useReducer(reducer, initial);
```

---

## Node.js

```js
// Built-in modules
import fs from 'node:fs/promises';
import path from 'node:path';
import { Readable, Transform } from 'node:stream';
import { randomBytes, scryptSync } from 'node:crypto';

// Read file
const data = await fs.readFile('./file.txt', 'utf8');

// Stream
import { createReadStream } from 'node:fs';
createReadStream('big.txt').pipe(process.stdout);

// HTTP server (no framework)
import { createServer } from 'node:http';
createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'application/json' });
  res.end(JSON.stringify({ ok: true }));
}).listen(3000);

// Env vars
const port = process.env.PORT ?? 3000;
```

---

## Express

```js
import express from 'express';
const app = express();

app.use(express.json());

app.get('/users/:id', async (req, res, next) => {
  try {
    const user = await getUser(req.params.id);
    if (!user) return res.status(404).json({ error: 'Not found' });
    res.json(user);
  } catch (err) { next(err); }
});

app.use((err, req, res, next) => {
  console.error(err);
  res.status(500).json({ error: 'Internal server error' });
});

app.listen(3000);
```

---

## Fetch API (universal)

```js
// Modern fetch (Node 18+ and browsers)
const res = await fetch('https://api.example.com/data', {
  headers: { Authorization: `Bearer ${token}` },
});
if (!res.ok) throw new Error(`HTTP ${res.status}`);
const data = await res.json();
```

---

## SQL (PostgreSQL)

```sql
-- SELECT
SELECT id, name, email FROM users WHERE active = true ORDER BY created_at DESC LIMIT 20;

-- JOIN
SELECT u.name, COUNT(o.id) AS order_count
FROM users u
LEFT JOIN orders o ON o.user_id = u.id
WHERE u.created_at > '2024-01-01'
GROUP BY u.id, u.name
HAVING COUNT(o.id) > 5
ORDER BY order_count DESC;

-- INSERT
INSERT INTO users (name, email) VALUES ('Alice', 'a@b.com') RETURNING id;

-- UPDATE
UPDATE users SET name = 'Bob' WHERE id = 1 RETURNING *;

-- DELETE
DELETE FROM users WHERE id = 1;

-- Upsert
INSERT INTO users (email, name) VALUES ('a@b.com', 'Alice')
ON CONFLICT (email) DO UPDATE SET name = EXCLUDED.name RETURNING *;

-- Transactions
BEGIN;
INSERT INTO accounts (id, balance) VALUES (1, 100);
UPDATE accounts SET balance = balance - 50 WHERE id = 1;
COMMIT;  -- or ROLLBACK;

-- CTE
WITH active_users AS (
  SELECT * FROM users WHERE active = true
)
SELECT * FROM active_users WHERE created_at > '2024-01-01';

-- Indexes
CREATE INDEX CONCURRENTLY idx_users_email ON users (email);
CREATE UNIQUE INDEX idx_users_email_unique ON users (lower(email));

-- JSONB
SELECT * FROM users WHERE preferences @> '{"theme": "dark"}';
SELECT data->'name' FROM events WHERE data->>'type' = 'signup';
```

---

## Redis

```bash
SET key value
GET key
DEL key
EXPIRE key 60        # 60 seconds
SETEX key 60 value   # set with TTL
INCR counter
HSET user:1 name Alice age 30
HGET user:1 name
LPUSH queue item
RPOP queue
SADD tags foo bar
SMEMBERS tags
ZADD leaderboard 100 alice 200 bob
ZREVRANGE leaderboard 0 9 WITHSCORES
PUBLISH channel message
SUBSCRIBE channel
```

---

## Git

```bash
# Setup
git config --global user.name "Name"
git config --global user.email "email@example.com"
git config --global init.defaultBranch main
git config --global pull.rebase true

# Daily
git status
git add .
git commit -m "feat: add login form"
git push origin main
git pull --rebase origin main

# Branching
git checkout -b feature/login
git switch feature/login
git switch -
git branch -d feature/login

# Stash
git stash
git stash pop
git stash list

# History
git log --oneline --graph --all
git log -p <file>
git blame <file>

# Undo
git restore <file>            # discard local changes
git restore --staged <file>   # unstage
git reset --soft HEAD~1       # undo last commit, keep changes staged
git reset --hard HEAD~1       # undo last commit, discard changes (CAREFUL)

# Reflog (lifesaver)
git reflog
git reset --hard HEAD@{5}

# Bisect
git bisect start
git bisect bad HEAD
git bisect good v1.0.0
# test, then:
git bisect good  # or bad
git bisect reset

# Amend
git commit --amend --no-edit
git commit --amend -m "new message"

# Cherry-pick
git cherry-pick <sha>

# Rebase
git rebase main
git rebase -i HEAD~3   # squash last 3

# Tags
git tag v1.0.0
git push origin v1.0.0
```

---

## Docker

```dockerfile
# Multi-stage Node Dockerfile
FROM node:20-alpine AS deps
WORKDIR /app
COPY package*.json ./
RUN npm ci

FROM node:20-alpine AS builder
WORKDIR /app
COPY --from=deps /app/node_modules ./node_modules
COPY . .
RUN npm run build

FROM node:20-alpine AS runner
WORKDIR /app
ENV NODE_ENV=production
RUN addgroup -g 1001 -S nodejs && adduser -S nextjs -u 1001
COPY --from=builder /app/public ./public
COPY --from=builder --chown=nextjs:nodejs /app/.next/standalone ./
COPY --from=builder --chown=nextjs:nodejs /app/.next/static ./.next/static
USER nextjs
EXPOSE 3000
CMD ["node", "server.js"]
```

```bash
docker build -t myapp .
docker run -p 3000:3000 myapp
docker compose up -d
docker compose logs -f
docker exec -it <container> sh
docker system prune -a
```

---

## GitHub Actions

```yaml
# .github/workflows/ci.yml
name: CI
on:
  push:
    branches: [main]
  pull_request:
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: npm
      - run: npm ci
      - run: npm run lint
      - run: npm run typecheck
      - run: npm run build
      - run: npm test
```

---

## cURL

```bash
# GET
curl https://api.example.com/data

# POST JSON
curl -X POST https://api.example.com/data \
  -H "Content-Type: application/json" \
  -d '{"name":"Alice"}'

# Auth
curl -H "Authorization: Bearer TOKEN" https://api.example.com/protected

# Cookies
curl -c cookies.txt -b cookies.txt https://example.com/login

# Follow redirects, show headers
curl -L -I https://example.com

# Download
curl -O https://example.com/file.zip
```

---

## Vim (emergency)

```
i           insert mode
Esc         normal mode
:wq         save & quit
:q!         quit without saving
dd          delete line
yy          yank line
p           paste
/text       search
n / N       next / prev match
u           undo
Ctrl-r      redo
gg / G      top / bottom of file
0 / $       start / end of line
```

---

## Shell

```bash
# Find by name (use ripgrep / fd instead)
rg "pattern"                 # search content
fd "name"                    # find files

# Process management
lsof -i :3000                # what's on port 3000
kill -9 <pid>
ps aux | grep node

# Networking
nc -zv example.com 443       # port check
dig example.com              # DNS
curl -I https://example.com  # headers

# File ops
tar -czf archive.tar.gz dir/
tar -xzf archive.tar.gz
zip -r archive.zip dir/
unzip archive.zip

# Disk
df -h
du -sh *

# System
top / htop
free -h
uname -a
```

---

## Regex

```
.              any char
\d \w \s       digit, word, whitespace
\D \W \S       negations
^ $            start, end
\b             word boundary
* + ?          0+, 1+, 0/1
{3} {3,} {2,5} exactly, at least, between
[abc] [a-z]    char class
[^abc]         negated class
(a|b)          alternation
(abc)          capture group
(?:abc)        non-capture
(?=abc)        lookahead
(?<=abc)       lookbehind
```

---

**Next:** [INDEX.md](INDEX.md) · [BEST_PRACTICES.md](BEST_PRACTICES.md) · [START-HERE.md](START-HERE.md)
