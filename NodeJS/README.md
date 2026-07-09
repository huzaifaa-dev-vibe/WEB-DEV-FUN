# Node.js

> JavaScript on the server. Event loop, streams, modules, clusters.

---

## Purpose

Master Node.js: event loop, streams, modules, clusters, performance.

## Prerequisites

- [JavaScript/](../JavaScript/).

## Learning Outcome

You can build, debug, and optimize production Node.js apps.

## Dependencies

- Node.js runtime.

## Related Files

- [JavaScript/](../JavaScript/) · [Express/](../Express/) · [Fastify/](../Fastify/) · [Bun/](../Bun/) · [Deno/](../Deno/) · [NodeJS/event-loop.md](event-loop.md) · [NodeJS/streams.md](streams.md)

## AI Instructions

When building Node apps:
1. **Async/await** for I/O. Never block the event loop.
2. **Streams** for large data.
3. **Cluster** or **worker threads** for CPU-bound work.
4. **Pino** for logging.
5. **Set timeouts** on all external calls.
6. **Graceful shutdown** on SIGTERM.
7. **Don't run as root.** Use a non-privileged user.
8. **Pin Node version** (`.nvmrc`).

## Human Notes

### Event loop
```
┌──────────────────────────┐
│   Call stack (sync)      │
├──────────────────────────┤
│   Microtasks (Promises)  │  ← drained after every task
├──────────────────────────┤
│   Timers (setTimeout)    │
├──────────────────────────┤
│   Poll (I/O callbacks)   │
├──────────────────────────┤
│   Check (setImmediate)   │
├──────────────────────────┤
│   Close callbacks        │
└──────────────────────────┘
```

→ [NodeJS/event-loop.md](event-loop.md)

### Don't block the event loop
- CPU-bound work: use worker_threads, child_process, or a separate service.
- Sync I/O: never in production.
- Large JSON.parse: streaming parser or worker.

### Streams
Process data in chunks, not all at once.
```js
import { createReadStream } from 'node:fs';
import { pipeline } from 'node:stream/promises';
import { createGunzip } from 'node:zlib';

await pipeline(
  createReadStream('data.gz'),
  createGunzip(),
  process.stdout
);
```

→ [NodeJS/streams.md](streams.md)

### Modules
- **CommonJS** (`require`) — legacy.
- **ES Modules** (`import`) — modern, default for new.
- `"type": "module"` in package.json to use ESM.

```js
// ESM
import fs from 'node:fs/promises';
import path from 'node:path';

export const readFile = async (file) => fs.readFile(file, 'utf8');
```

### Cluster (multi-process)
```js
import cluster from 'node:cluster';
import os from 'node:os';

if (cluster.isPrimary) {
  for (let i = 0; i < os.cpus().length; i++) cluster.fork();
} else {
  // start server
}
```
Or use `PM2` / systemd to manage processes.

### Worker threads
For CPU-bound work in same process.
```js
import { Worker } from 'node:worker_threads';

const worker = new Worker('./heavy.js', { workerData: { input: '...' } });
worker.on('message', (result) => console.log(result));
```

### Performance
- Use `--max-old-space-size=4096` for memory-heavy.
- `node --inspect` for DevTools.
- `clinic.js` for profiling.
- `0x` for flame graphs.

### HTTP server (no framework)
```js
import { createServer } from 'node:http';

const server = createServer(async (req, res) => {
  res.writeHead(200, { 'Content-Type': 'application/json' });
  res.end(JSON.stringify({ ok: true }));
});

server.listen(3000);
```

### File system
```js
import fs from 'node:fs/promises';

const data = await fs.readFile('./file.txt', 'utf8');
await fs.writeFile('./out.txt', data);
const files = await fs.readdir('./');
```

### Crypto
```js
import { randomBytes, scryptSync, timingSafeEqual } from 'node:crypto';

const salt = randomBytes(16);
const hash = scryptSync(password, salt, 64);
```

### Process
- `process.env` — env vars.
- `process.argv` — CLI args.
- `process.exit(code)` — exit (avoid; let event loop drain).
- `process.on('SIGTERM', ...)` — graceful shutdown.

### Common built-ins
- `node:fs` / `node:fs/promises`
- `node:path`
- `node:url`
- `node:http` / `node:https`
- `node:crypto`
- `node:stream`
- `node:buffer`
- `node:util`
- `node:os`
- `node:child_process`
- `node:worker_threads`
- `node:events`
- `node:net`
- `node:zlib`

### npm/pnpm
- Lockfile (`package-lock.json` / `pnpm-lock.yaml`) in git.
- `npm ci` for reproducible installs.
- `npm audit` for vulnerabilities.
- Don't commit `node_modules`.

### Node version managers
- `nvm`, `fnm`, `volta`, `mise`.
- Pin via `.nvmrc` or `package.json#engines`.

## Common Mistakes

- ❌ Sync I/O in production.
- ❌ No timeouts.
- ❌ Memory leaks (event listeners, closures).
- ❌ `process.exit()` instead of graceful shutdown.
- ❌ Running as root.
- ❌ Unhandled promise rejections.
- ❌ Global state.

## Tools

- PM2: process manager.
- Nodemon / tsx watch: dev restart.
- clinic.js: profiling.
- 0x: flame graphs.
- Winston / Pino: logging.
- Helmet: security headers.

## References

- Node.js docs: https://nodejs.org/api
- Node.js Best Practices: https://github.com/goldbergyoni/nodebestpractices
- Node.js design patterns: https://www.nodejsdesignpatterns.com/

## Further Reading

- *Node.js Design Patterns* — Mario Casciaro
- *Node.js the Right Way* — Jim Wilson

## Exercises

1. Build an HTTP server with no framework.
2. Stream a large file through gzip to a response.
3. Add graceful shutdown.
4. Profile a slow endpoint with clinic.js.

## Projects

- Build a file upload service with streaming.
- Build a worker pool for CPU-bound tasks.

---

**Previous:** [Backend/](../Backend/) · **Next:** [Bun/](../Bun/) · **Related:** [Express/](../Express/), [Fastify/](../Fastify/)
