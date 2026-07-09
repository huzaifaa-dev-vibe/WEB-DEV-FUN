# ROADMAP

> The complete curriculum, in dependency order. Follow the arrows.

This roadmap is a directed acyclic graph (DAG) of skills. Each node links to its folder. Arrows (`→`) indicate "do this before that". Asterisks (\*) indicate optional but recommended.

---

## Stage 0 — Foundations (everyone)

```
Internet Basics → HTTP → DNS → Browsers → Developer Tools
```

Read: [NOTES.md](NOTES.md#internet-fundamentals)

**Outcomes:** You can explain what happens between typing a URL and seeing a page. You can use DevTools Network tab.

---

## Stage 1 — Markup & Style

```
HTML (semantic) → Forms → Accessibility primitives
   │
   └→ CSS (selectors, box model, specificity)
         │
         ├→ Flexbox → Grid → Responsive Design → Container Queries
         │
         ├→ Typography → Color theory → Design tokens
         │
         └→ Animations (CSS) → Transitions → Keyframes
```

**Outcomes:** You can build a fully responsive, accessible, attractive static page by hand.

Folders: [HTML/](HTML/) · [CSS/](CSS/) · [Flexbox/](Flexbox/) · [Grid/](Grid/) · [Responsive-Design/](Responsive-Design/) · [Typography/](Typography/) · [Animations/](Animations/) · [Accessibility/](Accessibility/)

---

## Stage 2 — Interactivity

```
JavaScript (syntax, types) → DOM → Events → Fetch & async
   │
   ├→ Storage (localStorage, IndexedDB)
   │
   ├→ Web APIs (IntersectionObserver, ResizeObserver, WebSockets)
   │
   └→ TypeScript → Generics → Utility types → tsconfig
```

**Outcomes:** You can add interactivity, fetch data, persist state, and ship type-safe JS.

Folders: [JavaScript/](JavaScript/) · [TypeScript/](TypeScript/)

---

## Stage 3 — Frontend Framework

Pick ONE primary framework; learn the others later.

```
React → Hooks → State (Zustand/Redux) → React Query → React Router / Next.js
Vue  → Composition API → Pinia → Vue Router / Nuxt
Svelte → Stores → SvelteKit
Angular → Modules/Components → RxJS → Signals
```

**Outcomes:** You can build a SPA with routing, state, data fetching.

Folders: [UI/](UI/) · [EXTERNAL_REPOSITORIES.md](EXTERNAL_REPOSITORIES.md#frontend-frameworks)

---

## Stage 4 — Meta-frameworks & Rendering

```
SSR vs CSR vs SSG vs ISR → Next.js (App Router) → Server Actions → Streaming
                         → Nuxt → Astro (islands) → Qwik (resumability)*
```

**Outcomes:** You can pick the right rendering strategy and implement it.

Folders: [Templates/_next-app/](Templates/) · [SEO/](SEO/) · [Performance/](Performance/)

---

## Stage 5 — Design Systems & UI

```
Design tokens → Component library (shadcn/ui) → Storybook* → Design system docs
Color palettes → Typography scale → Spacing scale → Icon system
ANTI-AI-DESIGN principles (read BEFORE shipping any UI)
```

**Outcomes:** Your UI doesn't look AI-generated. You can build a coherent design system.

Folders: [ANTI-AI-DESIGN/](ANTI-AI-DESIGN/) · [UI/](UI/) · [UX/](UX/) · [Color-Palettes/](Color-Palettes/)

---

## Stage 6 — Backend Basics

```
HTTP servers → REST → Status codes → Idempotency → Versioning
Express or Fastify or Hono → Middleware → Error handling → Validation (Zod)
WebSockets → SSE → Long polling
```

**Outcomes:** You can build a JSON API with validation, errors, and real-time updates.

Folders: [Backend/](Backend/) · [APIs/](APIs/) · [REST/](REST/) · [NodeJS/](NodeJS/) · [Express/](Express/) · [Fastify/](Fastify/) · [WebSockets/](WebSockets/)

---

## Stage 7 — Databases & Persistence

```
SQL basics → PostgreSQL → Indexes → Migrations → Transactions
NoSQL → MongoDB (when to use)
Caching → Redis → Cache patterns (cache-aside, write-through)
ORM → Prisma or Drizzle → Schema design → N+1 problem
```

**Outcomes:** You can model data, write efficient queries, and avoid common pitfalls.

Folders: [Databases/](Databases/) · [PostgreSQL/](PostgreSQL/) · [MongoDB/](MongoDB/) · [Redis/](Redis/) · [Prisma/](Prisma/) · [Drizzle/](Drizzle/)

---

## Stage 8 — Authentication & Security

```
Sessions vs JWT vs OAuth vs Passkeys → Cookies → CSRF → CORS
OWASP Top 10 → XSS → SQL Injection → CSRF → SSRF → Rate limiting
CSP → HTTPS/HSTS → Secret management
```

**Outcomes:** You can implement secure auth and avoid the OWASP Top 10.

Folders: [Authentication/](Authentication/) · [Security/](Security/)

---

## Stage 9 — Testing

```
Test pyramid → Unit (Vitest) → Component (RTL) → E2E (Playwright)
Mocking → Snapshots (sparingly) → Visual regression*
Evals for AI features
```

**Outcomes:** You have a test suite that catches real bugs without slowing you down.

Folders: [Testing/](Testing/) · [Jest/](Jest/) · [Vitest/](Vitest/) · [Cypress/](Cypress/) · [Playwright/](Playwright/) · [E2E/](E2E/)

---

## Stage 10 — DevOps & Deployment

```
Git workflow → GitHub → Pull requests → Code review
Docker → docker-compose → Multi-stage builds
CI/CD → GitHub Actions → Preview deploys
Cloud pick: Vercel | Netlify | Cloudflare | AWS | Azure | GCP
Monitoring → Logs → Metrics → Traces → Alerts
```

**Outcomes:** You can ship safely, observe production, and roll back fast.

Folders: [Git/](Git/) · [Docker/](Docker/) · [CI-CD/](CI-CD/) · [Deployment/](Deployment/) · [Vercel/](Vercel/) · [Cloudflare/](Cloudflare/) · [AWS/](AWS/) · [Monitoring/](Monitoring/) · [Logging/](Logging/)

---

## Stage 11 — Architecture & Scale

```
Clean Code → SOLID → Design Patterns → Layered architecture → Hexagonal
System Design → Caching → Queues → CAP → Consistency models
Microservices → Service boundaries → Saga → Outbox → Event sourcing*
```

**Outcomes:** You can design a system that survives scale and change.

Folders: [Clean-Code/](Clean-Code/) · [Design-Patterns/](Design-Patterns/) · [Architecture/](Architecture/) · [System-Design/](System-Design/) · [Microservices/](Microservices/)

---

## Stage 12 — AI Engineering (optional, fast-growing)

```
LLM fundamentals → Prompt engineering → Function calling → Structured output
RAG → Embeddings → Vector DBs → Chunking strategies
Agents → Tool use → Planning → Reflection
MCP servers → Agentic IDEs (Cursor, Cline, Aider)
Evals → Cost & latency → Safety
```

**Outcomes:** You can ship LLM features that don't hallucinate or bankrupt you.

Folders: [AI/](AI/) · [LLM/](LLM/) · [MCP/](MCP/) · [Agentic-Coding/](Agentic-Coding/) · [Prompt-Engineering/](Prompt-Engineering/)

---

## Cross-cutting — Always Relevant

| Topic | Folder |
|---|---|
| Performance budgets & Web Vitals | [Performance/](Performance/) |
| SEO & schema | [SEO/](SEO/) |
| Analytics & privacy | [Analytics/](Analytics/) |
| Accessibility audits | [Accessibility/](Accessibility/) |
| Pre-launch checklists | [Checklists/](Checklists/) |
| Common mistakes | [COMMON_MISTAKES.md](COMMON_MISTAKES.md) |
| Anti-patterns | [ANTI-PATTERNS.md](ANTI-PATTERNS.md) |

---

## Timeline Suggestion (Part-time, 10h/week)

| Weeks | Stage |
|---|---|
| 1–3 | 0 + 1 |
| 4–6 | 2 |
| 7–10 | 3 + 4 |
| 11–12 | 5 |
| 13–16 | 6 + 7 |
| 17–18 | 8 |
| 19–20 | 9 + 10 |
| 21–24 | 11 + Capstone |
| 25+ | 12 (AI) or specialize |

---

**Next:** [INDEX.md](INDEX.md) · [START-HERE.md](START-HERE.md) · [AI_AGENT_GUIDE.md](AI_AGENT_GUIDE.md)
