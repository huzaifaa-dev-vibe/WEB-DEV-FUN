# Bun

> All-in-one JavaScript runtime. Fast. Built-in bundler, test runner, package manager.

---

## Purpose

Use Bun as a faster alternative to Node.js with built-in tools.

## Prerequisites

- [JavaScript/](../JavaScript/).

## Learning Outcome

You can use Bun for runtime, package management, testing, and bundling.

## Dependencies

- Bun installed.

## Related Files

- [NodeJS/](../NodeJS/) · [Deno/](../Deno/) · [JavaScript/](../JavaScript/)

## AI Instructions

When using Bun:
1. `bun install` (faster than npm).
2. `bun run script.ts` (no compilation step).
3. `bun test` (built-in test runner).
4. `bun build` (bundler).
5. Note: Bun is fast but ecosystem is younger than Node. Verify library compat.

## Human Notes

### What Bun replaces
- Node.js (runtime).
- npm/pnpm/yarn (package manager).
- tsx/ts-node (TS runner).
- Vitest/Jest (test runner).
- esbuild/webpack (bundler).
- nodemon (dev server).

### Install
```bash
curl -fsSL https://bun.sh/install | bash
```

### Use
```bash
bun install              # install deps
bun add zod              # add dep
bun run index.ts         # run TS directly
bun test                 # run tests
bun build ./index.ts --outdir ./dist  # bundle
```

### Built-in APIs
```ts
// Bun.serve (HTTP server)
Bun.serve({
  port: 3000,
  fetch(req) {
    return new Response('Hello!');
  },
});

// Bun.file (file I/O, fast)
const file = Bun.file('./data.json');
const text = await file.text();

// Bun.password (hashing)
const hash = await Bun.password.hash('password');
const valid = await Bun.password.verify('password', hash);

// Bun.write
await Bun.write('./out.txt', 'content');
```

### Compatibility
- Mostly Node-compatible.
- Some Node APIs missing or different.
- Many npm packages work; check https://bun.sh/docs/runtime/nodejs-apis

### When to use
- New projects, greenfield.
- Scripts (fast startup).
- When you want one tool.
- Edge / serverless (small cold start).

### When NOT to use
- Heavy Node ecosystem dependency.
- Production-critical with no fallback.
- Need long-term LTS guarantees (Bun is younger).

### Elysia (Bun-first framework)
```ts
import { Elysia } from 'elysia';

new Elysia()
  .get('/', () => 'Hello!')
  .post('/users', ({ body }) => createUser(body))
  .listen(3000);
```

## Common Mistakes

- ❌ Assuming 100% Node compat.
- ❌ Using Bun for production-critical without fallback.
- ❌ Not testing deps work with Bun.

## Tools

- Bun docs: https://bun.sh/docs
- Elysia: https://elysiajs.com/

## References

- Bun: https://bun.sh/

## Exercises

1. Rewrite a Node script in Bun. Compare speed.
2. Build an API with Elysia.

## Projects

- Build a real-time app with Bun + WebSockets.

---

**Previous:** [NodeJS/](../NodeJS/) · **Next:** [Deno/](../Deno/) · **Related:** [JavaScript/](../JavaScript/)
