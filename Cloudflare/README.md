# Cloudflare

> Edge network with Workers, Pages, R2, D1, KV, and more. Cheap and fast.

---

## Purpose

Use Cloudflare's edge platform for global, low-latency apps.

## Prerequisites

- Cloudflare account.

## Learning Outcome

You can deploy Workers, Pages, and use Cloudflare's storage and security services.

## Dependencies

- Cloudflare account.

## Related Files

- [Vercel/](../Vercel/) · [Netlify/](../Netlify/) · [AWS/](../AWS/) · [Deployment/](../Deployment/)

## AI Instructions

When using Cloudflare:
1. **Workers** for edge compute (V8 isolates, global).
2. **Pages** for static sites.
3. **R2** for S3-compatible object storage (no egress fees).
4. **D1** for serverless SQLite.
5. **KV** for global key-value.
6. **Durable Objects** for stateful edge.
7. **Queues** for message queues.
8. **Cache API** for fine-grained caching.
9. **WARP** for client VPN.
10. **Zero Trust** for app access.

## Human Notes

### Workers
```ts
// src/index.ts
export default {
  async fetch(request: Request, env: Env): Promise<Response> {
    return new Response('Hello from edge!');
  },
};
```

```bash
npx wrangler init myapp
npx wrangler deploy
npx wrangler tail
```

### Workers + Hono
```ts
import { Hono } from 'hono';

const app = new Hono();
app.get('/', (c) => c.text('Hello!'));

export default app;
```

### Pages
- Static sites + Functions.
- Connect Git or use `wrangler pages deploy`.

### R2 (S3-compatible, no egress fees)
```ts
const obj = await env.MY_BUCKET.put('key', 'value');
const obj = await env.MY_BUCKET.get('key');
```

### D1 (serverless SQLite)
```ts
const stmt = env.DB.prepare('SELECT * FROM users WHERE id = ?');
const user = await stmt.bind(1).first();
```

### KV (global key-value)
```ts
await env.MY_KV.put('key', 'value');
const value = await env.MY_KV.get('key');
```

### Durable Objects
Stateful edge objects. For real-time, multiplayer, etc.

### Queues
Message queue for async work.

### Cache API
```ts
const cache = caches.default;
await cache.put(request, response);
const cached = await cache.match(request);
```

### Cloudflare DNS
- Free.
- Fast.
- Anycast.
- API-accessible.

### Cloudflare CDN
- Free tier.
- Cache static assets at edge.
- Page Rules / Cache Rules for fine control.

### Cloudflare for SaaS
- Custom domains per customer.
- SSL for everyone.

### Zero Trust
- Replace VPN with identity-aware proxy.
- Free for small teams.

### When to use Cloudflare
- Edge-first apps (global, low latency).
- Cheaper than AWS for storage (R2 = no egress).
- DDoS protection.
- DNS / CDN.
- Workers for serverless at edge.

### When NOT to use
- Long-running CPU (Workers have CPU limits).
- Need AWS-specific services.

## Common Mistakes

- ❌ Exceeding CPU limits (Workers are short).
- ❌ Not using R2 for storage (S3 egress fees add up).
- ❌ Not using KV for cache.
- ❌ Not using Cloudflare DNS (slow DNS elsewhere).

## Tools

- Cloudflare docs: https://developers.cloudflare.com/
- Wrangler CLI: https://developers.cloudflare.com/workers/wrangler/
- Cloudflare dashboard.

## References

- Cloudflare blog: https://blog.cloudflare.com/
- Workers docs: https://developers.cloudflare.com/workers/

## Further Reading

- Cloudflare Weekly: https://weekly.cloudflare.com/

## Exercises

1. Deploy a Worker with Hono.
2. Set up R2 + D1.
3. Build a real-time app with Durable Objects.

## Projects

- Build an edge-deployed API with Workers + D1 + R2.

---

**Previous:** [Netlify/](../Netlify/) · **Next:** [AWS/](../AWS/) · **Related:** [Deployment/](../Deployment/)
