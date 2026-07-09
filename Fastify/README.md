# Fastify

> High-performance Node.js web framework. Schema-based, plugin architecture.

---

## Purpose

Build fast, schema-validated APIs with Fastify.

## Prerequisites

- [NodeJS/](../NodeJS/), [Express/](../Express/) (for comparison).

## Learning Outcome

You can build a Fastify app with plugins, schemas, and hooks.

## Dependencies

- Node.js.

## Related Files

- [Express/](../Express/) · [NestJS/](../NestJS/) · [NodeJS/](../NodeJS/) · [APIs/](../APIs/)

## AI Instructions

When using Fastify:
1. Use JSON schemas for validation (faster than Zod for runtime, but less type-safe).
2. Use TypeScript with `fastify-type-provider-zod` for Zod integration.
3. Use plugins for organization.
4. Use hooks (`onRequest`, `preHandler`) for auth, logging.
5. Built-in Pino logger.

## Human Notes

### Why Fastify over Express
- 2x+ faster.
- Schema validation built-in.
- Plugin architecture.
- Better TypeScript support.
- Built-in logger (Pino).

### Basic app
```ts
import Fastify from 'fastify';

const app = Fastify({ logger: true });

app.get('/health', async () => ({ ok: true }));

app.post('/users', {
  schema: {
    body: {
      type: 'object',
      required: ['name', 'email'],
      properties: {
        name: { type: 'string' },
        email: { type: 'string', format: 'email' },
      },
    },
  },
}, async (req, reply) => {
  return { id: 1, ...req.body };
});

app.listen({ port: 3000 });
```

### With Zod
```ts
import Fastify from 'fastify';
import { ZodTypeProvider, jsonSchema, serializerCompiler, validatorCompiler } from 'fastify-type-provider-zod';
import { z } from 'zod';

const app = Fastify().withTypeProvider<ZodTypeProvider>();
app.setValidatorCompiler(validatorCompiler);
app.setSerializerCompiler(serializerCompiler);

app.post('/users', {
  schema: {
    body: z.object({
      name: z.string(),
      email: z.string().email(),
    }),
  },
}, async (req) => {
  return { id: 1, ...req.body }; // typed!
});
```

### Plugins
```ts
app.register(async (instance, opts) => {
  instance.get('/users', async () => [/* ... */]);
}, { prefix: '/api' });
```

### Hooks
```ts
app.addHook('onRequest', async (req, reply) => {
  // auth check
  req.user = verifyToken(req.headers.authorization);
});

app.addHook('preHandler', async (req) => {
  // before handler
});

app.addHook('onError', async (req, reply, error) => {
  req.log.error({ err: error });
});
```

### Schema-based serialization
Fastify serializes responses using JSON schemas — faster than `JSON.stringify`.

### When to use Fastify
- High-throughput APIs.
- Want schema validation.
- Want structured logging built-in.

### When NOT to use
- Need batteries-included (use NestJS).
- Need Angular-style DI (use NestJS).

## Common Mistakes

- ❌ Not using schemas (loses Fastify's perf advantage).
- ❌ Mixing Zod and JSON schema confusingly.
- ❌ Not using plugins (everything in one file).

## Tools

- Fastify docs: https://fastify.dev/docs/
- Fastify ecosystem: https://fastify.dev/ecosystem/

## References

- Fastify: https://fastify.dev/

## Exercises

1. Build a CRUD API with Zod schemas.
2. Add auth via onRequest hook.
3. Compare perf vs Express.

## Projects

- Build a high-throughput API with Fastify + Redis cache.

---

**Previous:** [Express/](../Express/) · **Next:** [NestJS/](../NestJS/) · **Related:** [NodeJS/](../NodeJS/)
