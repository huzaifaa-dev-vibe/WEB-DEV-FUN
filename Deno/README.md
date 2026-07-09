# Deno

> Secure-by-default JavaScript runtime. TypeScript native. By Node's creator.

---

## Purpose

Use Deno as a secure, modern alternative to Node.

## Prerequisites

- [JavaScript/](../JavaScript/), [TypeScript/](../TypeScript/).

## Learning Outcome

You can build apps with Deno, leverage its security model, and use Deno Deploy.

## Dependencies

- Deno installed.

## Related Files

- [NodeJS/](../NodeJS/) · [Bun/](../Bun/) · [JavaScript/](../JavaScript/)

## AI Instructions

When using Deno:
1. TypeScript native — no setup.
2. Permissions model: `--allow-net`, `--allow-read`, etc.
3. Std library: `import { serve } from 'std/http/server.ts'`.
4. Use Deno Deploy for edge hosting.
5. Compatible with npm packages via `npm:` specifiers.

## Human Notes

### Install
```bash
curl -fsSL https://deno.land/install.sh | sh
```

### Use
```bash
deno run app.ts                  # run with prompts for permissions
deno run --allow-net app.ts      # allow network
deno run --allow-all app.ts      # allow everything (defeats purpose)
deno test                        # built-in test runner
deno fmt                         # formatter
deno lint                        # linter
deno compile app.ts              # single-binary output
```

### Built-in
- TypeScript native (no compilation step).
- Test runner.
- Formatter (like Prettier).
- Linter.
- Bundler.
- Compiler (single binary).

### Permissions model
Deno prompts before:
- Network access.
- File read/write.
- Env access.
- Subprocess.
- High-res time.

Explicit grant via flags. Secure by default.

### Standard library
```ts
import { serve } from 'https://deno.land/std/http/server.ts';

serve((req) => new Response('Hello!'), { port: 8000 });
```

### npm compatibility
```ts
import express from 'npm:express@4';
```

### Hono (works on Deno)
```ts
import { Hono } from 'https://deno.land/x/hono/mod.ts';

const app = new Hono();
app.get('/', (c) => c.text('Hello!'));
Deno.serve(app.fetch);
```

### Deno Deploy
- Edge hosting (like Cloudflare Workers).
- Free tier.
- Global, low latency.

### When to use
- Want security model.
- Want edge deployment.
- TypeScript native.
- Fewer dependencies.

### When NOT to use
- Heavy Node ecosystem.
- Existing Node codebase.
- Need npm-specific tooling.

## Common Mistakes

- ❌ `--allow-all` everywhere (defeats purpose).
- ❌ Not using the std library.
- ❌ Mixing URL imports and npm imports confusingly.

## Tools

- Deno docs: https://deno.land/manual
- Deno Deploy: https://deno.com/deploy

## References

- Deno: https://deno.com/
- Deno Std: https://deno.land/std

## Exercises

1. Build an API with Deno + Hono.
2. Deploy to Deno Deploy.

## Projects

- Build an edge-deployed app with Deno Deploy.

---

**Previous:** [Bun/](../Bun/) · **Next:** [Express/](../Express/) · **Related:** [NodeJS/](../NodeJS/)
