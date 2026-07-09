# System Design

> Scale, consistency, CAP, caching, queues. The big picture.

---

## Purpose

Design systems that scale, survive failures, and stay consistent.

## Prerequisites

- [Backend/](../Backend/), [Databases/](../Databases/), [Architecture/](../Architecture/).

## Learning Outcome

You can design a system for a given scale, pick the right trade-offs, and explain your choices.

## Dependencies

- None (conceptual).

## Related Files

- [Architecture/](../Architecture/) · [Microservices/](../Microservices/) · [Databases/](../Databases/) · [System-Design/resilience.md](resilience.md) · [EXTERNAL_REPOSITORIES.md](../EXTERNAL_REPOSITORIES.md)

## AI Instructions

When designing systems:
1. **Understand requirements**: users, RPS, data volume, latency.
2. **Start simple** (monolith). Add complexity only when forced.
3. **Boring tech** for the 80% case.
4. **Pick consistency model** based on needs.
5. **Cache aggressively**, invalidate carefully.
6. **Queue for decoupling**.
7. **Design for failure**: timeouts, retries, circuit breakers.
8. **Document trade-offs** as ADRs.

## Human Notes

### Key concepts

#### CAP theorem
- Consistency.
- Availability.
- Partition tolerance.

In distributed systems with partitions, you choose C or A. Most web apps choose AP with eventual consistency.

#### ACID vs BASE
- ACID: strong consistency, traditional RDBMS.
- BASE: eventual consistency, NoSQL.

#### Consistency models
- Strong (linearizable).
- Sequential.
- Causal.
- Eventual.
- Read-your-writes.
- Monotonic reads.

#### Scaling
- **Vertical** (bigger machine) — easy, limited.
- **Horizontal** (more machines) — harder, scales further.

#### Load balancing
- L4 (TCP) — fast, dumb.
- L7 (HTTP) — smart, content-aware.
- Algorithms: round-robin, least connections, IP hash, weighted.

#### Caching
- **Cache-aside** — app reads cache, then DB.
- **Write-through** — write to cache + DB.
- **Write-behind** — write to cache, async to DB.
- **CDN** — edge cache.
- **Browser** — HTTP cache.
- **DB** — Postgres shared buffers, Redis.

Cache invalidation is hard. TTL + explicit invalidation.

#### Queues
- Decouple producers from consumers.
- Smooth spikes.
- Allow retries.
- Tools: SQS, RabbitMQ, NATS, Kafka, Redis (BullMQ).

#### Database scaling
- **Read replicas** for read scale.
- **Sharding** for write scale (last resort).
- **CQRS** for different read/write models.
- **Event sourcing** for audit + replay (rare).

#### Distributed transactions
- **2PC** (two-phase commit) — slow, blocking.
- **Saga** — sequence of local transactions with compensations.
- **Outbox pattern** — write event + state in same transaction, then publish.

#### Idempotency
- All write endpoints should be idempotent.
- Use Idempotency-Key header.

#### Backpressure
- Don't accept work faster than you can process.
- Drop, queue, or signal slow.

### Resilience patterns
- **Timeouts** — on everything.
- **Retries** with exponential backoff + jitter.
- **Circuit breaker** — stop calling failing service.
- **Bulkhead** — isolate failures.
- **Rate limiter** — protect from overload.
- **Graceful degradation** — partial functionality.
- **Fail fast** — don't make users wait.

→ [System-Design/resilience.md](resilience.md)

### Common patterns
- **Load-balanced stateless services** behind a LB.
- **Database + read replicas**.
- **Cache layer** (Redis).
- **Queue** for async work.
- **CDN** for static assets.
- **Object storage** (S3) for files.
- **Search** (Elasticsearch, Meilisearch) for full-text.
- **Analytics warehouse** (BigQuery, ClickHouse) for analytics.

### Back-of-envelope numbers
- L1 cache: 0.5 ns
- L2 cache: 7 ns
- Mutex lock: 25 ns
- Main memory: 100 ns
- 1KB Zippy compress: 3 μs
- SSD random read: 150 μs
- Read 1MB from SSD: 1 ms
- Network same DC: 0.5 ms
- Read 1MB from network: 10 ms
- Disk seek: 10 ms
- Round trip CA→Netherlands: 150 ms

Source: https://gist.github.com/jboner/2841832

### Estimation
- Daily active users → RPS ( rough: DAU × sessions × actions / 86400 × peak factor).
- Storage: rows × row size × growth.
- Bandwidth: requests × response size × RPS.

## Common Mistakes

- ❌ Premature microservices.
- ❌ No timeouts.
- ❌ No retries / circuit breakers.
- ❌ Synchronous chains.
- ❌ Shared DB across services.
- ❌ Cache without invalidation strategy.
- ❌ No idempotency.
- ❌ Scaling before measuring.

## Tools

- Drawing: Excalidraw, Eraser, Whimsical.
- ADRs: markdown.

## References

- ByteByteGo: https://bytebytego.com/
- System Design Primer: https://github.com/donnemartin/system-design-primer
- Designing Data-Intensive Applications (book).
- High Scalability: https://highscalability.com/

## Further Reading

- *Designing Data-Intensive Applications* — Martin Kleppmann
- *System Design Interview* — Alex Xu
- *Building Microservices* — Sam Newman
- *Release It!* — Michael Nygard

## Exercises

1. Design Twitter (timeline, fanout, scale).
2. Design a URL shortener.
3. Design a chat app.
4. Design a rate limiter.

## Projects

- Design and build a URL shortener at scale (1B URLs, 10k RPS).

---

**Previous:** [Clean-Code/](../Clean-Code/) · **Next:** [Architecture/](../Architecture/) · **Related:** [Microservices/](../Microservices/)
