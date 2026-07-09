# Backend

> The server side. Where data lives, business logic runs, and APIs are born.

---

## Purpose

Master backend concepts: HTTP servers, middleware, validation, errors, logging, background jobs.

## Prerequisites

- [JavaScript/](../JavaScript/) or another server language.

## Learning Outcome

You can build a production backend with any framework.

## Dependencies

- A runtime (Node / Bun / Deno / Python / Go / Rust / etc.).

## Related Files

- [NodeJS/](../NodeJS/) · [Express/](../Express/) · [Fastify/](../Fastify/) · [NestJS/](../NestJS/) · [APIs/](../APIs/) · [REST/](../REST/) · [Security/](../Security/) · [Databases/](../Databases/) · [Authentication/](../Authentication/)

## AI Instructions

When building backends:
1. **Validate at the edge** (Zod/Valibot on every input).
2. **Use proper HTTP status codes.**
3. **Structured logging** with request IDs.
4. **Rate limit** public endpoints.
5. **Don't trust the client.**
6. **Timeouts on everything** (DB, external API, request).
7. **Idempotency keys** for mutations.
8. **Transactions** for multi-step writes.
9. **Background jobs** for slow work (email, processing).
10. **Health checks** (`/health`, `/ready`).

## Human Notes

### The 12-Factor App
→ https://12factor.net/

1. **Codebase** — one codebase per app, many deploys.
2. **Dependencies** — explicit, isolated.
3. **Config** — env vars, not code.
4. **Backing services** — treat as attached resources (DB, cache, email).
5. **Build, release, run** — separate stages.
6. **Processes** — stateless, share nothing.
7. **Port binding** — self-contained HTTP service.
8. **Concurrency** — via processes.
9. **Disposability** — fast startup, graceful shutdown.
10. **Dev/prod parity** — similar envs.
11. **Logs** — event stream.
12. **Admin processes** — one-off tasks.

### Layered architecture
```
HTTP layer (routes, middleware)
    ↓
Application layer (use cases, orchestration)
    ↓
Domain layer (business logic, entities)
    ↓
Infrastructure (DB, external APIs, etc.)
```

Dependency direction: top → bottom.

### Middleware
```js
app.use((req, res, next) => {
  req.id = crypto.randomUUID();
  const start = Date.now();
  res.on('finish', () => {
    logger.info({ id: req.id, method: req.method, path: req.path, status: res.statusCode, ms: Date.now() - start });
  });
  next();
});
```

### Validation
```js
import { z } from 'zod';

const CreateUserSchema = z.object({
  name: z.string().min(1).max(100),
  email: z.string().email(),
  age: z.number().int().min(13).max(150).optional(),
});

app.post('/users', async (req, res) => {
  const result = CreateUserSchema.safeParse(req.body);
  if (!result.success) {
    return res.status(400).json({ error: { code: 'VALIDATION_ERROR', details: result.error.flatten() } });
  }
  // result.data is typed
});
```

### Error handling
- Throw typed errors.
- Central error middleware.
- Never expose internals.
- Log everything.

```js
class HttpError extends Error {
  constructor(status, code, message) {
    super(message);
    this.status = status;
    this.code = code;
  }
}

app.use((err, req, res, next) => {
  logger.error({ id: req.id, err });
  if (err instanceof HttpError) {
    return res.status(err.status).json({ error: { code: err.code, message: err.message } });
  }
  res.status(500).json({ error: { code: 'INTERNAL', message: 'Something went wrong' } });
});
```

### Background jobs
- Don't make users wait for email sends, image processing, etc.
- Use a queue (BullMQ, Temporal, SQS).
- Worker process consumes.

### Health checks
- `/health` — liveness (is process up?).
- `/ready` — readiness (can I take traffic? DB connected?).

### Graceful shutdown
- On SIGTERM:
  1. Stop accepting new connections.
  2. Finish in-flight requests.
  3. Close DB pools.
  4. Exit.

### Logging
- Structured (JSON).
- Request ID for correlation.
- Levels: debug, info, warn, error.
- Never log secrets/PII.
- → [Logging/](../Logging/)

### Configuration
- Env vars for everything environment-specific.
- Validate at startup (Zod).
- Don't hard-code.

### Security
- → [Security/](../Security/)
- Helmet for headers.
- Rate limiting.
- CORS allowlist.
- Input validation.
- Parameterized SQL.
- Hash passwords.

### Testing
- Unit tests for logic.
- Integration tests for endpoints (with real DB or test DB).
- → [Testing/](../Testing/)

## Common Mistakes

- ❌ Trusting client input.
- ❌ No timeouts.
- ❌ No rate limiting.
- ❌ Sync I/O in Node event loop.
- ❌ No graceful shutdown.
- ❌ Logging PII.
- ❌ 200 for errors.
- ❌ Hard-coded config.

## Tools

- See specific framework folders.

## References

- 12-Factor App: https://12factor.net/
- Web.dev backend: https://web.dev/learn/forms
- OWASP: https://owasp.org/

## Further Reading

- *Designing Web APIs* — Brenda Jin et al.
- *Release It!* — Michael Nygard
- *Designing Data-Intensive Applications* — Martin Kleppmann

## Exercises

1. Build a JSON API with validation, errors, logging, health check.
2. Add background jobs for email.
3. Add graceful shutdown.

## Projects

- Build a complete backend for a SaaS app.

---

**Previous:** [WebSockets/](../WebSockets/) · **Next:** [NodeJS/](../NodeJS/) · **Related:** [APIs/](../APIs/)
