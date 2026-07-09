# ANTI-PATTERNS

> Architectural & design anti-patterns. Bigger than mistakes — these are systemic traps.

Where [COMMON_MISTAKES.md](COMMON_MISTAKES.md) covers tactical errors, this file covers strategic ones: architectures, organizational choices, and design philosophies that look reasonable in isolation but compound into failure.

---

## Architecture Anti-Patterns

### 🚫 The Big Ball of Mud
**Symptom:** No clear structure. Code anywhere. Dependencies everywhere.
**Why it happens:** "Just get it done" without refactor time.
**Consequence:** Change ripples. Fear of refactoring. Velocity drops to zero.
**Fix:** Introduce module boundaries one at a time. Define a dependency direction. See [Architecture/](Architecture/).

### 🚫 The Distributed Monolith
**Symptom:** "Microservices" that all deploy together, share a database, and break if any one is down.
**Why it happens:** Cargo-culting microservices.
**Consequence:** All the costs of microservices, none of the benefits.
**Fix:** Start monolithic. Split only when a service has a different scale, deploy cadence, or team ownership. → [Microservices/](Microservices/)

### 🚫 Premature Microservices
**Symptom:** 3-person team maintaining 12 services.
**Why it happens:** Resume-driven development.
**Consequence:** Operational nightmare. Latency multiplies. Bugs span services.
**Fix:** One service per team (at minimum). → [Microservices/when-to-split.md](Microservices/when-to-split.md)

### 🚫 The Anemic Domain Model
**Symptom:** "Models" are just data bags. All logic in services.
**Why it happens:** CRUD mindset.
**Consequence:** Logic duplicated across services. Models drift.
**Fix:** Put behavior on the entities that own the data. → [Architecture/ddd.md](Architecture/ddd.md)

### 🚫 The God Object / God Component
**Symptom:** One file/class/component does everything.
**Why it happens:** Adding to existing instead of extracting.
**Consequence:** No one can modify safely. Tests are huge.
**Fix:** Split by responsibility. → [Clean-Code/srp.md](Clean-Code/srp.md)

### 🚫 The Golden Hammer
**Symptom:** "We use X for everything."
**Why it happens:** Team familiarity > fitness for purpose.
**Consequence:** Forcing wrong tool into wrong job.
**Fix:** Have 2–3 tools in your belt. Pick by fitness. → [EXTERNAL_REPOSITORIES.md](EXTERNAL_REPOSITORIES.md)

---

## Frontend Anti-Patterns

### 🚫 The Mega-Bundle
**Symptom:** First-load JS > 1MB for a content site.
**Why it happens:** No code-splitting. Re-exported barrel files. Heavy deps.
**Consequence:** Slow. Bounced users. SEO penalty.
**Fix:** Bundle analyzer. Per-route splitting. Replace heavy deps. → [Performance/budgets.md](Performance/budgets.md)

### 🚫 Prop Drilling Hell
**Symptom:** State passed through 5+ component layers.
**Why it happens:** No global state strategy.
**Consequence:** Refactor hell. Re-renders.
**Fix:** Context, store, or co-locate. → [UI/state.md](UI/state.md)

### 🚫 Effect-Driven State
**Symptom:** `useEffect` writing to state derived from other state.
**Why it happens:** Thinking imperatively.
**Consequence:** Cascade renders. Stale state. Race conditions.
**Fix:** Derive in render. Use state machines for complex flows.

### 🚫 The Custom Design System That's Just Re-skinning shadcn
**Symptom:** "We have our own design system" — it's 80 components that wrap Radix with different class names.
**Why it happens:** NIH syndrome.
**Consequence:** Maintenance burden. Drift from upstream fixes.
**Fix:** Just use shadcn/ui or contribute upstream.

### 🚫 Reinventing Forms
**Symptom:** Hand-rolled form validation, submission, error handling.
**Why it happens:** "Forms are easy."
**Consequence:** Edge cases missed. Accessibility bad.
**Fix:** React Hook Form + Zod. Or TanStack Form. → [EXTERNAL_REPOSITORIES.md](EXTERNAL_REPOSITORIES.md#forms)

### 🚫 Inline Styles for Everything
**Symptom:** `style={{ ... }}` everywhere.
**Why it happens:** Quick fixes.
**Consequence:** No theming. No responsive. No pseudo-states.
**Fix:** Tailwind / CSS Modules / vanilla-extract.

---

## Backend Anti-Patterns

### 🚫 The Single-Page API
**Symptom:** `/api` does everything based on payload shape.
**Why it happens:** "REST is too complex."
**Consequence:** No caching. No idempotency. No tooling.
**Fix:** REST resources or proper GraphQL. → [REST/](REST/), [GraphQL/](GraphQL/)

### 🚫 The Leaky Abstraction
**Symptom:** Your ORM exposes SQL concepts; your API exposes DB schema.
**Why it happens:** No boundary design.
**Consequence:** Schema changes break clients. Hard to evolve.
**Fix:** Separate internal model from external DTO. → [Architecture/layers.md](Architecture/layers.md)

### 🚫 Shared Database Across Services
**Symptom:** Multiple services reading/writing the same tables.
**Why it happens:** "Easier than sync."
**Consequence:** Coupling. Migration hell.
**Fix:** One DB per service. Sync via events/APIs. → [Microservices/data-ownership.md](Microservices/data-ownership.md)

### 🚫 The "Magic" Framework Layer
**Symptom:** Decorators/annotations do so much that no one knows what runs when.
**Why it happens:** Framework zealotry.
**Consequence:** Debugging is archaeology.
**Fix:** Prefer explicit over implicit. Limit magic to one layer.

### 🚫 Synchronous Chains
**Symptom:** Request → service A → service B → service C → DB. All sync.
**Why it happens:** Easier than queues.
**Consequence:** Latency stacks. Cascading failures.
**Fix:** Async where you can. Circuit breakers. Timeouts. → [System-Design/resilience.md](System-Design/resilience.md)

### 🚫 No Timeouts
**Symptom:** Calls to external APIs with no timeout.
**Why it happens:** Defaults left in place.
**Consequence:** Hanging requests. Pool exhaustion.
**Fix:** Always set timeouts. Aggressive for user-facing, generous for batch.

---

## Database Anti-Patterns

### 🚫 The Entity-Attribute-Value (EAV) Model
**Symptom:** One table for all "attributes" with entity_id, attr_name, attr_value.
**Why it happens:** "Flexible schema!"
**Consequence:** Slow queries. No type safety. Nightmare joins.
**Fix:** Real columns. JSONB for genuinely dynamic data. → [PostgreSQL/jsonb.md](PostgreSQL/jsonb.md)

### 🚫 The Polymorphic Association
**Symptom:** `parent_id` + `parent_type` columns.
**Why it happens:** ActiveRecord-style "easy" associations.
**Consequence:** No FK constraints. Orphaned rows.
**Fix:** Real FKs. Or join tables per type.

### 🚫 Storing Files in the DB
**Symptom:** Images/PDFs as BLOBs.
**Why it happens:** "Easier backup."
**Consequence:** DB bloat. Slow queries. RAM exhaustion.
**Fix:** Object storage (S3, R2). Store URL in DB.

### 🚫 No Soft-Delete Strategy (or soft-delete everywhere)
**Symptom:** Either everything is hard-deleted (data loss) or everything has `deleted_at` (queries everywhere leak).
**Why it happens:** No thought given to data lifecycle.
**Fix:** Decide per table. Use a tool/framework that handles it. Or event sourcing.

### 🚫 One Giant Transactional DB for Everything
**Symptom:** Analytics queries locking up the prod transactional DB.
**Why it happens:** "Just query prod."
**Consequence:** Slow prod. Slow analytics.
**Fix:** Read replica for analytics. Or warehouse (BigQuery, ClickHouse, Snowflake).

### 🚫 UUID v4 Clustered Index
**Symptom:** Random UUID PKs on a high-write table.
**Why it happens:** Default UUID generator.
**Consequence:** Index fragmentation. Slow inserts.
**Fix:** UUID v7 / ULID / bigserial. → [PostgreSQL/uuids.md](PostgreSQL/uuids.md)

---

## Security Anti-Patterns

### 🚫 Security Through Obscurity
**Symptom:** "It's secure because nobody knows the URL."
**Why it happens:** Hope.
**Consequence:** Someone finds it. Catastrophe.
**Fix:** Authn/Authz on every endpoint. Always.

### 🚫 Roll-Your-Own Crypto
**Symptom:** Custom encryption / hashing / token logic.
**Why it happens:** "Just need something simple."
**Consequence:** Broken in 100 ways you can't see.
**Fix:** Use vetted libraries. bcrypt/argon2. JWT libs. TLS.

### 🚫 The Permissive CORS
**Symptom:** `Access-Control-Allow-Origin: *` with credentials.
**Why it happens:** "It doesn't work otherwise."
**Consequence:** Any site can be the user.
**Fix:** Allowlist. → [Security/cors.md](Security/cors.md)

### 🚫 Logging Everything Including Secrets
**Symptom:** Full request bodies in logs.
**Why it happens:** Debugging convenience.
**Consequence:** Breach amplification. Compliance violation.
**Fix:** Redact PII/secrets. Structured logging with allowlist. → [Logging/redaction.md](Logging/redaction.md)

### 🚫 Trusting the Client
**Symptom:** Client decides authorization (e.g., `if (user.role === 'admin')`).
**Why it happens:** Quick prototypes ship to prod.
**Consequence:** Anyone can be admin.
**Fix:** Server enforces everything. Client only renders.

### 🚫 No Rate Limiting on Auth Endpoints
**Symptom:** Login endpoint takes unlimited requests.
**Why it happens:** "We'll add it later."
**Consequence:** Credential stuffing.
**Fix:** Rate limit per IP + per user. Exponential backoff. → [Security/rate-limiting.md](Security/rate-limiting.md)

---

## Process Anti-Patterns

### 🚫 The Hero Culture
**Symptom:** One dev carries the project. Late nights. "Only X can fix this."
**Why it happens:** Reward heroics over steady progress.
**Consequence:** Burnout. Bus factor = 1.
**Fix:** Distribute knowledge. Pair. Rotate on-call. Document.

### 🚫 Estimate-Driven Development
**Symptom:** Dates drive scope and quality.
**Why it happens:** Pressure from above.
**Consequence:** Tech debt. Cut corners. Burnout.
**Fix:** Scope drives dates. Or fix scope and let dates flex. → [NOTES.md](NOTES.md#estimation)

### 🚫 The Waterfall Sprint
**Symptom:** 2 weeks of design → 2 weeks of dev → 2 weeks of QA.
**Why it happens:** "Agile" in name only.
**Consequence:** Late integration. Surprises.
**Fix:** Vertical slices. Demo weekly.

### 🚫 Meetings as Status Reports
**Symptom:** Daily standup is just "what I did yesterday."
**Why it happens:** Habit.
**Consequence:** Wasted time. No problem-solving.
**Fix:** Async standups. Use meetings for decisions and unblocks.

### 🚫 No Technical Strategy
**Symptom:** "Just build features."
**Why it happens:** Tactical pressure.
**Consequence:** Architecture drift. Velocity decay.
**Fix:** Quarterly tech strategy. RFCs for big changes. → [Architecture/rfcs.md](Architecture/rfcs.md)

### 🚫 Skipping Post-Mortems
**Symptom:** Incidents happen, nobody writes anything down.
**Why it happens:** Busy.
**Consequence:** Same incidents repeat.
**Fix:** Blameless post-mortem within 48h. → [Checklists/post-mortem.md](Checklists/post-mortem.md)

---

## AI Engineering Anti-Patterns

### 🚫 The "Just Wrap GPT-4" Product
**Symptom:** Thin wrapper around an LLM API, no moat.
**Why it happens:** Easy MVP.
**Consequence:** Commoditized overnight. No defensible value.
**Fix:** Add domain data, workflows, integrations, evals, UX.

### 🚫 Prompt-Injected Product
**Symptom:** User input directly in the system prompt.
**Why it happens:** "It's just a chatbot."
**Consequence:** "Ignore previous instructions and..."
**Fix:** Treat user content as data. → [Security/ai.md](Security/ai.md)

### 🚫 No Evals, Just Vibes
**Symptom:** "It looks good to me."
**Why it happens:** Evals are unglamorous.
**Consequence:** Every prompt change is roulette.
**Fix:** Eval set. Run on every change. Track metrics. → [AI/evals.md](AI/evals.md)

### 🚫 The Infinite Loop Agent
**Symptom:** Agent runs for 30 minutes, $50 later, no result.
**Why it happens:** No max iterations, no budget cap.
**Consequence:** Money burn. Bad UX.
**Fix:** Hard limits on tokens, iterations, cost. → [Performance/ai-cost.md](Performance/ai-cost.md)

### 🚫 The Black-Box Production Agent
**Symptom:** Agent does things, nobody knows what.
**Why it happens:** "It works."
**Consequence:** Can't debug. Can't improve. Can't trust.
**Fix:** Log every step, every tool call, every output. Tracing. → [Agentic-Coding/observability.md](Agentic-Coding/observability.md)

### 🚫 One Giant Prompt
**Symptom:** 4000-token system prompt doing 17 things.
**Why it happens:** Adding instead of refactoring.
**Consequence:** Hard to debug. Conflicting instructions.
**Fix:** Split into roles. Or use multi-agent.

---

## Design Anti-Patterns

### 🚫 The Template Look
**Symptom:** Site looks like 10,000 other SaaS sites.
**Why it happens:** Same templates, same defaults.
**Consequence:** No brand. No memory.
**Fix:** → [ANTI-AI-DESIGN/](ANTI-AI-DESIGN/)

### 🚫 The Cover-Everything-in-Animation Site
**Symptom:** Everything fades in, slides up, parallax-scrolls.
**Why it happens:** "It looks cool."
**Consequence:** Distracting. Motion sickness. Slow.
**Fix:** Animate to explain. Respect `prefers-reduced-motion`.

### 🚫 The Feature Dump Homepage
**Symptom:** 30 features listed above the fold.
**Why it happens:** "We need to show value."
**Consequence:** Nothing stands out.
**Fix:** One promise. One proof. One CTA. → [ANTI-AI-DESIGN/hero-alternatives.md](ANTI-AI-DESIGN/hero-alternatives.md)

### 🚫 The Generic Empty State
**Symptom:** Empty states say "No data" or worse, "Lorem ipsum".
**Why it happens:** Afterthought.
**Consequence:** Users don't know what to do.
**Fix:** Empty states explain + offer a next action.

---

**Next:** [ERRORS.md](ERRORS.md) · [DEBUGGING.md](DEBUGGING.md) · [COMMON_MISTAKES.md](COMMON_MISTAKES.md)
