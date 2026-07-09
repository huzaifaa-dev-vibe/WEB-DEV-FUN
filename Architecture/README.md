# Architecture

> Decisions that are expensive to change. Patterns, layers, ADRs.

---

## Purpose

Architect systems that scale, evolve, and stay maintainable.

## Prerequisites

- Built at least one production app.

## Learning Outcome

You can architect a system, justify trade-offs, and document decisions.

## Dependencies

- None (conceptual).

## Related Files

- [ARCHITECTURE.md](../ARCHITECTURE.md) · [System-Design/](../System-Design/) · [Microservices/](../Microservices/) · [Clean-Code/](../Clean-Code/) · [Design-Patterns/](../Design-Patterns/) · [Architecture/adrs.md](adrs.md) · [Architecture/ddd.md](ddd.md) · [Architecture/layers.md](layers.md)

## AI Instructions

When architecting:
1. **Start monolith** unless you have a real reason for microservices.
2. **Modular monolith** with clear module boundaries.
3. **Layered architecture** (presentation / application / domain / infrastructure).
4. **Dependency direction**: top → bottom. Domain depends on nothing.
5. **Document every non-trivial decision** as an ADR.
6. **Don't add a layer/pattern** unless it pays for itself.

## Human Notes

→ See [ARCHITECTURE.md](../ARCHITECTURE.md) for the full overview.

### Patterns
- **Layered** — presentation / application / domain / infrastructure.
- **Hexagonal (Ports & Adapters)** — domain isolated from infra.
- **Clean Architecture** — dependencies point inward.
- **Onion Architecture** — similar to Clean.
- **CQRS** — separate read/write models.
- **Event Sourcing** — store events, derive state.
- **Microservices** — multiple services, team-owned.
- **Modular Monolith** — single deployable, modular code.

### ADRs
```markdown
# ADR-001: Use Postgres as primary DB

## Status
Accepted (2025-01-15)

## Context
We need a relational DB. Team knows Postgres.

## Decision
Postgres.

## Consequences
+ ACID, JSONB, free, mature.
- Less horizontal scale than Mongo for some workloads.
Mitigation: read replicas.

## Alternatives considered
MySQL: less features.
MongoDB: schemaless, wrong fit.
```

→ [Architecture/adrs.md](adrs.md)

### When to use what
| Need | Pattern |
|---|---|
| Most apps | Modular monolith + layered |
| Multiple teams, scale | Microservices |
| Need full audit | Event sourcing |
| Read-heavy, different R/W | CQRS |
| Want domain isolated | Hexagonal |

### Domain-Driven Design (DDD)
- Ubiquitous language.
- Bounded contexts.
- Aggregates.
- Entities / Value objects.
- Repositories.

→ [Architecture/ddd.md](ddd.md)

### RFCs
For big changes:
1. Author writes RFC.
2. Comments for N days.
3. Decision.
4. ADR.

→ [Architecture/rfcs.md](rfcs.md)

### Diagrams
- C4 model (Context, Container, Component, Code).
- Sequence diagrams.
- ER diagrams.
- Architecture diagrams.

→ [Architecture/diagrams.md](diagrams.md)

## Common Mistakes

- ❌ Premature microservices.
- ❌ God module.
- ❌ No ADRs.
- ❌ Layer violations.
- ❌ Big bang rewrites.
- ❌ Architecture astronautics.

## Tools

- Excalidraw, Eraser, Whimsical, draw.io.

## References

- martinfowler.com: https://martinfowler.com/
- 12-factor: https://12factor.net/
- C4 model: https://c4model.com/

## Further Reading

- *Designing Data-Intensive Applications* — Kleppmann
- *A Philosophy of Software Design* — Ousterhout
- *Software Architecture: The Hard Parts* — Ford et al.
- *Building Evolutionary Architectures* — Ford, Parsons, Kua

## Exercises

1. Write an ADR for a recent decision.
2. Map your app's layers. Identify violations.
3. Draw a C4 diagram of your system.

## Projects

- Refactor a monolith into a modular monolith.

---

**Previous:** [System-Design/](../System-Design/) · **Next:** [Microservices/](../Microservices/) · **Related:** [Clean-Code/](../Clean-Code/)
