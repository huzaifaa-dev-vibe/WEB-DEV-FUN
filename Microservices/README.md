# Microservices

> Multiple services, team-owned. Powerful but expensive. Use with caution.

---

## Purpose

Know when to split, how to split, and how to operate microservices.

## Prerequisites

- [Architecture/](../Architecture/), [System-Design/](../System-Design/).

## Learning Outcome

You can decide if microservices fit, design service boundaries, and operate them.

## Dependencies

- Distributed systems infrastructure.

## Related Files

- [Architecture/](../Architecture/) · [System-Design/](../System-Design/) · [Microservices/when-to-split.md](when-to-split.md) · [Microservices/data-ownership.md](data-ownership.md) · [ANTI-PATTERNS.md#architecture-anti-patterns](../ANTI-PATTERNS.md)

## AI Instructions

When considering microservices:
1. **Default to monolith** unless you have a real reason.
2. **One service per team** (minimum).
3. **Each service owns its data** (no shared DB).
4. **Async communication** (events/queues) over sync (HTTP).
5. **Idempotency** for all writes.
6. **Outbox pattern** for reliable event publishing.
7. **Saga** for distributed transactions.
8. **Observability** across services (traces).

## Human Notes

### When to split
- Multiple teams (≥2 per service).
- Different scale requirements.
- Different deploy cadence.
- Different tech stack needed.
- Clear bounded context.

→ [Microservices/when-to-split.md](when-to-split.md)

### When NOT to split
- Single team.
- MVP / startup.
- Tightly coupled domain.
- "I want to learn microservices."

### Patterns

#### Database per service
- Each service owns its data.
- No shared DB.
- Sync via events or API.

→ [Microservices/data-ownership.md](data-ownership.md)

#### API composition
- Service A calls B, C, D to compose a response.
- Watch for latency.

#### Saga
- Distributed transaction.
- Sequence of local transactions.
- Compensations on failure.

#### Outbox pattern
- Write event + state in same transaction.
- Separate process publishes events.
- Reliable event publishing.

#### Service discovery
- Service registry (Consul, etcd, Kubernetes DNS).
- Client-side load balancing.

#### API Gateway
- Single entry point.
- Auth, rate limit, routing.
- BFF (Backend for Frontend) per client.

#### Circuit breaker
- Stop calling failing service.
- Fail fast.

#### Service mesh
- Istio, Linkerd.
- mTLS, traffic control, observability.

### Communication
- **Sync (HTTP/gRPC)** — simple, but coupling.
- **Async (events/messages)** — decoupled, eventual consistency.
- Prefer async for cross-service.

### Data consistency
- **Strong** — hard across services.
- **Eventual** — normal in microservices.
- **Saga** for distributed transactions.

### Observability
- Distributed tracing (OpenTelemetry).
- Correlation IDs.
- Centralized logs.
- Per-service metrics.

### Deployment
- Independent deploys.
- Containerized.
- Orchestrated (K8s, ECS, Nomad).

### Testing
- Unit per service.
- Contract tests (Pact) for cross-service.
- E2E for critical paths only (slow).

## Common Mistakes

- ❌ Premature microservices.
- ❌ Distributed monolith (shared DB, sync chains).
- ❌ No service boundaries (just technical split).
- ❌ No observability.
- ❌ No idempotency.
- ❌ Synchronous chains.
- ❌ Shared libraries that couple services.

## Tools

- Kubernetes, Istio, Linkerd.
- Kafka, NATS, RabbitMQ.
- OpenTelemetry.
- Pact (contract tests).

## References

- martinfowler.com microservices: https://martinfowler.com/articles/microservices.html
- Sam Newman's work.

## Further Reading

- *Building Microservices* — Sam Newman
- *Monolith to Microservices* — Sam Newman
- *Microservices Patterns* — Chris Richardson

## Exercises

1. Identify a bounded context in your system. Could it be a service?
2. Design a saga for order placement.
3. Implement outbox pattern.

## Projects

- Build a small e-commerce system with 3 services (users, orders, inventory) using events.

---

**Previous:** [Architecture/](../Architecture/) · **Next:** [Testing/](../Testing/) · **Related:** [System-Design/](../System-Design/)
