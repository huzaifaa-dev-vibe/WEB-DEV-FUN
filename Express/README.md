# Express

> The minimal, unopinionated Node.js web framework. Mature, ubiquitous, simple.

---

## Purpose

Build HTTP APIs and servers with Express.

## Prerequisites

- [NodeJS/](../NodeJS/), [JavaScript/](../JavaScript/) or [TypeScript/](../TypeScript/).

## Learning Outcome

You can build a production Express app with middleware, validation, error handling, and tests.

## Dependencies

- Node.js.

## Related Files

- [NodeJS/](../NodeJS/) · [Fastify/](../Fastify/) · [NestJS/](../NestJS/) · [APIs/](../APIs/) · [REST/](../REST/)

## AI Instructions

When using Express:
1. Use Express 5 (or 4.19+) — handles async errors.
2. `helmet` for security headers.
3. `express-rate-limit` for rate limiting.
4. Zod for input validation.
5. Pino for logging.
6. Central error middleware.
7. Health check endpoints.
8. Graceful shutdown.

## Human Notes

### Basic app
```ts
import express from 'express';
import helmet from 'helmet';
import pino from 'pino';
import { z } from 'zod';

const app = express();
app.use(helmet());
app.use(express.json());

const logger = pino();

const CreateUser = z.object({
  name: z.string().min(1),
  email: z.string().email(),
});

app.post('/users', async (req, res, next) => {
  try {
    const data = CreateUser.parse(req.body);
    // create user
    res.status(201).json({ id: 1, ...data });
  } catch (err) {
    next(err);
  }
});

app.get('/health', (req, res) => res.json({ ok: true }));

// Central error handler
app.use((err, req, res, next) => {
  logger.error({ err });
  if (err instanceof z.ZodError) {
    return res.status(400).json({ error: { code: 'VALIDATION', details: err.flatten() } });
  }
  res.status(500).json({ error: { code: 'INTERNAL' } });
});

app.listen(3000);
```

### Middleware
- Order matters.
- `app.use(fn)` — global.
- `app.use('/path', fn)` — path-scoped.
- `app.get('/path', fn1, fn2, handler)` — route-specific.

### Common middleware
- `helmet` — security headers.
- `cors` — CORS.
- `express.json()` — parse JSON body.
- `express.urlencoded()` — parse form body.
- `morgan` / `pino-http` — logging.
- `express-rate-limit` — rate limit.
- `cookie-parser` — cookies.
- `express-session` — sessions.
- `compression` — gzip.

### Async errors
Express 5 handles async errors automatically. Express 4 needs `express-async-errors` or wrappers.

### Routing
```ts
import { Router } from 'express';

const router = Router();
router.get('/', getUsers);
router.post('/', createUser);

app.use('/api/users', router);
```

### Validation
- Don't use `express-validator` (older). Use Zod.

### Performance
- Express is slow compared to Fastify.
- For high-throughput APIs, consider Fastify.

### When NOT to use
- Need speed: Fastify.
- Need structure/opinions: NestJS.
- Edge: Hono.
- Bun: Elysia.

## Common Mistakes

- ❌ No error middleware.
- ❌ No async error handling (Express 4).
- ❌ No body limits.
- ❌ No rate limiting.
- ❌ No security headers.
- ❌ Trusting `req.body` without validation.

## Tools

- Express docs: https://expressjs.com/
- Express middleware list: https://expressjs.com/en/resources/middleware.html

## References

- Express: https://expressjs.com/

## Further Reading

- *Express in Action* — Evan Hahn

## Exercises

1. Build a CRUD API with validation and errors.
2. Add rate limiting and security headers.
3. Add structured logging.

## Projects

- Build a complete REST API for a SaaS.

---

**Previous:** [Deno/](../Deno/) · **Next:** [Fastify/](../Fastify/) · **Related:** [NodeJS/](../NodeJS/)
