# Redis

> In-memory data structure store. Cache, queue, pub/sub, streams, and more.

---

## Purpose

Use Redis for caching, queues, sessions, rate limiting, real-time.

## Prerequisites

- [Databases/](../Databases/).

## Learning Outcome

You can use Redis for cache, pub/sub, streams, and as a primary data store for ephemeral data.

## Dependencies

- Redis 7+.

## Related Files

- [Databases/](../Databases/) · [PostgreSQL/](../PostgreSQL/) · [WebSockets/](../WebSockets/) · [Backend/](../Backend/)

## AI Instructions

When using Redis:
1. Use as cache (cache-aside pattern) — set TTL.
2. Use as queue (BullMQ, Sidekiq).
3. Use as session store.
4. Use for rate limiting (sorted sets / Lua scripts).
5. Use for pub/sub (real-time).
6. Don't use as primary DB (unless ephemeral data).
7. Use Upstash for serverless.
8. Set maxmemory + eviction policy.

## Human Notes

### Data structures
- **String** — value up to 512MB.
- **List** — ordered, doubly-linked.
- **Hash** — field-value map.
- **Set** — unique elements.
- **Sorted Set** — scored, ordered set.
- **Stream** — append-only log (Kafka-like).
- **Bitmap / HyperLogLog** — specialized.
- **Geo** — lat/long.

### Common patterns

#### Cache-aside
```js
async function getUser(id) {
  const cached = await redis.get(`user:${id}`);
  if (cached) return JSON.parse(cached);
  const user = await db.user.findUnique({ where: { id } });
  await redis.set(`user:${id}`, JSON.stringify(user), 'EX', 3600);
  return user;
}
```

#### Counter
```js
await redis.incr('page:views');
```

#### Rate limiting (sliding window)
```lua
-- Lua script for atomic rate limit
local key = KEYS[1]
local limit = tonumber(ARGV[1])
local window = tonumber(ARGV[2])
local current = redis.call('ZCARD', key)
if current >= limit then return 0 end
redis.call('ZADD', key, ARGV[3], ARGV[3])
redis.call('EXPIRE', key, window)
return 1
```

#### Queue (BullMQ)
```js
import { Queue, Worker } from 'bullmq';

const queue = new Queue('email', { connection: redis });
await queue.add('send', { to: 'a@b.com', subject: 'Hi' });

new Worker('email', async (job) => {
  await sendEmail(job.data);
}, { connection: redis });
```

#### Pub/sub
```js
// Publisher
await redis.publish('chat-room-1', 'Hello!');

// Subscriber
await subscriber.subscribe('chat-room-1');
subscriber.on('message', (channel, message) => {
  console.log(channel, message);
});
```

#### Sessions
```js
app.use(session({
  store: new RedisStore({ client: redis }),
  secret: process.env.SESSION_SECRET,
  cookie: { secure: true, httpOnly: true, sameSite: 'lax' },
}));
```

#### Leaderboard
```js
await redis.zadd('leaderboard', 100, 'alice', 200, 'bob');
const top = await redis.zrevrange('leaderboard', 0, 9, 'WITHSCORES');
```

#### Streams (Kafka-like)
```js
await redis.xadd('events', '*', 'type', 'signup', 'user', 'alice');
const events = await redis.xread('STREAMS', 'events', '0');
```

### Persistence
- **RDB** — point-in-time snapshots.
- **AOF** — append-only log.
- Both — for durability.

For pure cache: disable persistence. For queue: enable AOF.

### Replication
- Primary + replicas.
- Sentinel for HA.
- Cluster for sharding.

### Eviction policies
- `noeviction` — errors on OOM.
- `allkeys-lru` — evict least recently used.
- `allkeys-lfu` — evict least frequently used.
- `volatile-lru` — only keys with TTL.
- `volatile-ttl` — evict soonest TTL.

For cache: `allkeys-lru`. For queue: `noeviction`.

### Performance
- Single-threaded (mostly).
- 100k+ ops/sec on a single instance.
- Pipelines for batched commands.
- Lua scripts for atomic ops.

### Common mistakes
- ❌ No TTL on cache (memory grows forever).
- ❌ No eviction policy.
- ❌ Using as primary DB without persistence.
- ❌ Big keys (multi-MB values).
- ❌ Blocking commands (`KEYS *`) on prod.

## Tools

- Redis docs: https://redis.io/docs/
- Redis Insight: https://redis.io/insight/
- ioredis (Node): https://github.com/redis/ioredis
- BullMQ: https://docs.bullmq.io/
- Upstash: https://upstash.com/ (serverless)

## Further Reading

- *Redis in Action* — Josiah Carlson

## Exercises

1. Build a cache layer for a slow API.
2. Build a rate limiter with Redis + Lua.
3. Build a real-time chat with pub/sub.

## Projects

- Build a queue-based email system with BullMQ.

---

**Previous:** [MongoDB/](../MongoDB/) · **Next:** [SQLite/](../SQLite/) · **Related:** [Databases/](../Databases/)
