# ARCHITECTURE (Overview)

> The decisions that are expensive to change. Deep coverage in [Architecture/](Architecture/), [System-Design/](System-Design/), [Microservices/](Microservices/), [Clean-Code/](Clean-Code/), [Design-Patterns/](Design-Patterns/).

---

## Purpose

Architecture is the set of decisions that are hard to reverse. Get them right early. Get them wrong and you'll pay for years.

## Prerequisites

- Built at least one production app.
- Familiarity with the layers of a typical web app.

## Learning Outcome

You can design a system's structure, justify trade-offs, document decisions (ADRs), and evolve architecture without rewrites.

## Related Files

- [Architecture/](Architecture/) — patterns & principles
- [System-Design/](System-Design/) — scale
- [Microservices/](Microservices/) — service boundaries
- [Clean-Code/](Clean-Code/) — code-level structure
- [Design-Patterns/](Design-Patterns/) — GoF + reactive
- [ANTI-PATTERNS.md](ANTI-PATTERNS.md)
- [NOTES.md](NOTES.md)

## AI Instructions

When designing a new system:
1. Read [Architecture/README.md](Architecture/README.md) for patterns.
2. Read [System-Design/README.md](System-Design/README.md) for scale considerations.
3. Don't default to microservices. Default to modular monolith. Split only when forced.
4. Document every non-trivial decision as an ADR. → [Architecture/adrs.md](Architecture/adrs.md)
5. Don't introduce a layer/framework/pattern unless it pays for itself.

## Human Notes

### Layers of a typical web app
```
┌─────────────────────────────────┐
│  Presentation (UI, API)         │
├─────────────────────────────────┤
│  Application (use cases)        │
├─────────────────────────────────┤
│  Domain (business logic)        │
├─────────────────────────────────┤
│  Infrastructure (DB, external)  │
└─────────────────────────────────┘
```

Dependency direction: top → bottom. Domain depends on nothing (it's pure logic). Infrastructure implements interfaces the domain defines.

### When to add a layer
- When the cost of NOT having it exceeds the cost of having it.
- "For testability" — yes.
- "For future flexibility" — usually no. YAGNI.

### Architecture styles (when to use)
| Style | When |
|---|---|
| **Modular monolith** | Default. Most apps. Most teams. |
| **Microservices** | Multiple teams, different scale/deploy cadence per service. |
| **Event-driven** | Loose coupling, real-time, multiple consumers. |
| **CQRS** | Read-heavy with different read/write models. |
| **Event sourcing** | When you need full audit history. (Rare.) |
| **Hexagonal / Ports & Adapters** | When you want your domain independent of frameworks. |
| **Serverless** | Spiky traffic, low operational appetite. |

### Principles
- **SOLID** → [Clean-Code/solid.md](Clean-Code/solid.md)
- **DRY** — but not at the cost of clarity.
- **KISS** — complexity kills.
- **YAGNI** — don't build it until you need it.
- **Law of Demeter** — don't chain `a.b.c.d`.
- **Composition over inheritance.**
- **Push decisions late.** Decide at the last responsible moment.

### ADRs (Architecture Decision Records)
Every non-trivial decision = an ADR.

```markdown
# ADR-001: Use PostgreSQL as primary database

## Status
Accepted (2024-01-15)

## Context
We need a relational database for the core domain. The team is familiar with Postgres. We considered MySQL and MongoDB.

## Decision
Use PostgreSQL.

## Consequences
- Pro: ACID, JSONB, mature, free.
- Con: Less horizontal scale than Mongo for some workloads.
- Mitigation: read replicas for read-heavy cases.

## Alternatives considered
- MySQL: less feature-rich (no JSONB), fewer extension options.
- MongoDB: schemaless is wrong fit for our domain.
```

→ [Architecture/adrs.md](Architecture/adrs.md)

## Quick Picks for Common Situations

| Situation | Default |
|---|---|
| New app, small team | Modular monolith, Postgres, Next.js |
| Need real-time | WebSocket server + Redis pub/sub |
| Need background jobs | BullMQ (Node) / Sidekiq (Ruby) / Celery (Python) / Temporal |
| Need search | Postgres FTS to start → Meilisearch/Typesense → Elasticsearch at scale |
| Need file storage | Cloudflare R2 / S3 |
| Need email | Resend / Postmark |
| Need payments | Stripe |
| Need auth | Clerk (B2C SaaS) / Auth0 / custom sessions |
| Need cache | Redis (Upstash managed) |
| Need queue | Redis (BullMQ) / SQS / NATS |
| Need logs | Axiom / Loki / Datadog |
| Need metrics | Prometheus + Grafana |
| Need errors | Sentry |
| Need traces | OpenTelemetry + Tempo / Jaeger |
| Need feature flags | PostHog / Unleash / Flagsmith |

## References

- *Designing Data-Intensive Applications* — Martin Kleppmann
- *A Philosophy of Software Design* — John Ousterhout
- *Software Architecture: The Hard Parts* — Ford, Richards, Sadalage, Dehghani
- *Building Evolutionary Architectures* — Ford, Parsons, Kua
- martinfowler.com: https://martinfowler.com/
- 12-factor app: https://12factor.net/

## Exercises

1. Take an existing app. Map its layers. Identify violations of dependency direction.
2. Write an ADR for a recent decision.
3. Pick a service in your system. Could it be split? Why or why not?

## Projects

- Build a modular monolith with clear module boundaries.
- Implement hexagonal architecture for a small API.

---

**Next:** [Architecture/](Architecture/) · [System-Design/](System-Design/) · [Microservices/](Microservices/)
