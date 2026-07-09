# START HERE

> Pick your track. Follow the path. Build something real.

This file is the entry point for every reader. Don't read the whole repo linearly — that would take weeks. Instead, find your track below and follow the prescribed sequence. Each track is ~30–60 hours of focused work to reach "job-ready" competence, or ~3–6 hours for an experienced engineer to skim and fill gaps.

---

## Step 1 — Pick a Track

| Track | You are... | Goal | Hours |
|---|---|---|---|
| **A. Beginner → Frontend** | New to code | Build & ship responsive websites | 40–60h |
| **B. Frontend → Full-stack** | Comfortable with JS/CSS | Build apps with auth, DB, deploy | 30–50h |
| **C. Backend-leaning** | Like servers, data, APIs | Build APIs & services end-to-end | 30–50h |
| **D. Designer → Builder** | Strong visual eye, weak code | Translate designs into production UI | 25–40h |
| **E. AI Engineer** | Want to build LLM-powered apps | Ship AI features safely | 20–40h |
| **F. AI Agent** | You are an LLM coding assistant | Use this repo as a reference manual | Read [AI_AGENT_GUIDE.md](AI_AGENT_GUIDE.md) |

---

## Step 2 — Set Up Your Workbench

Regardless of track, install these once:

```bash
# Runtimes
node --version    # >= 20 LTS
bun --version     # >= 1.1
python --version  # >= 3.11

# Editor: VS Code (recommended) with:
#   - ESLint, Prettier
#   - Tailwind CSS IntelliSense
#   - GitLens
#   - Error Lens
#   - Docker

# CLI essentials
gh auth login
git config --global init.defaultBranch main
git config --global pull.rebase true
```

See [TOOLS.md](TOOLS.md) for the full recommended toolkit.

---

## Track A — Beginner → Frontend

> Goal: build & ship a responsive, accessible website from scratch.

1. **Internet fundamentals** — how browsers, DNS, HTTP work. Read [NOTES.md](NOTES.md#internet-fundamentals).
2. **HTML** — semantic markup, forms, accessibility primitives. → [HTML/](HTML/)
3. **CSS foundations** — selectors, box model, specificity. → [CSS/](CSS/)
4. **Layout** — Flexbox then Grid. → [Flexbox/](Flexbox/), [Grid/](Grid/)
5. **Responsive design** — mobile-first, container queries. → [Responsive-Design/](Responsive-Design/)
6. **JavaScript essentials** — DOM, events, fetch, async. → [JavaScript/](JavaScript/)
7. **Accessibility** — WCAG, ARIA, keyboard nav. → [Accessibility/](Accessibility/)
8. **Performance** — Web Vitals, image optimization. → [Performance/](Performance/)
9. **Anti-AI design** — make it look human. → [ANTI-AI-DESIGN/](ANTI-AI-DESIGN/)
10. **Ship it** — deploy to Vercel or Netlify. → [Deployment/](Deployment/), [Vercel/](Vercel/)

**Capstone project:** Build a portfolio site. Blueprint: [Website-Blueprints/portfolio.md](Website-Blueprints/portfolio.md).

---

## Track B — Frontend → Full-stack

> Goal: build apps with auth, database, and CI/CD.

1. **TypeScript** — types, generics, narrowing. → [TypeScript/](TypeScript/)
2. **React** (or Vue/Svelte) — components, hooks, state. → [UI/](UI/)
3. **Next.js** — routing, SSR/SSG, server actions. → [Templates/_next-app/](Templates/)
4. **APIs** — REST design, status codes, idempotency. → [REST/](REST/)
5. **Authentication** — sessions vs JWT vs OAuth vs Passkeys. → [Authentication/](Authentication/)
6. **Databases** — relational vs document vs cache. → [Databases/](Databases/)
7. **ORM** — Prisma or Drizzle. → [Prisma/](Prisma/), [Drizzle/](Drizzle/)
8. **Testing** — unit (Vitest), E2E (Playwright). → [Testing/](Testing/), [Playwright/](Playwright/)
9. **CI/CD** — GitHub Actions. → [CI-CD/](CI-CD/)
10. **Deploy** — Vercel, Cloudflare, AWS. → [Deployment/](Deployment/)

**Capstone project:** Build a SaaS app with auth, billing, dashboard. Blueprint: [Website-Blueprints/saas.md](Website-Blueprints/saas.md).

---

## Track C — Backend-leaning

> Goal: design & operate APIs and services that scale.

1. **HTTP & networking** — methods, status, TLS, cookies. → [APIs/](APIs/)
2. **Node.js or alternative runtime** — event loop, streams. → [NodeJS/](NodeJS/) or [Go/](Go/) or [Rust/](Rust/)
3. **Framework** — Express / Fastify / NestJS / FastAPI / Axum. → respective folders.
4. **Databases** — Postgres + Redis as the default pair. → [PostgreSQL/](PostgreSQL/), [Redis/](Redis/)
5. **Architecture** — layered, hexagonal, ports & adapters. → [Architecture/](Architecture/), [Clean-Code/](Clean-Code/)
6. **System design** — caching, queues, consistency. → [System-Design/](System-Design/)
7. **Microservices** — when to split, saga, outbox. → [Microservices/](Microservices/)
8. **Auth** — OAuth, JWT, RBAC. → [Authentication/](Authentication/)
9. **Observability** — logs, metrics, traces. → [Monitoring/](Monitoring/), [Logging/](Logging/)
10. **Operate** — Docker, K8s, zero-downtime deploys. → [Docker/](Docker/), [Kubernetes/](Kubernetes/)

**Capstone project:** Build a URL shortener at scale. Spec: [Projects/url-shortener.md](Projects/url-shortener.md).

---

## Track D — Designer → Builder

> Goal: ship production-quality UI from Figma.

1. **Skip ahead** — you already know color, type, hierarchy. Skim [UI/](UI/) and [UX/](UX/) for vocabulary.
2. **HTML & CSS** — semantic markup, layout. → [HTML/](HTML/), [CSS/](CSS/)
3. **Tailwind** — utility-first workflow. → [CSS/](CSS/tailwind.md) (covered inside CSS folder)
4. **Component libraries** — shadcn/ui, Radix. → [EXTERNAL_REPOSITORIES.md](EXTERNAL_REPOSITORIES.md#component-libraries)
5. **Anti-AI design** — the most important folder for you. → [ANTI-AI-DESIGN/](ANTI-AI-DESIGN/)
6. **Framer Motion** — animation that feels human. → [Animations/](Animations/)
7. **Accessibility** — keyboard, screen readers, contrast. → [Accessibility/](Accessibility/)

**Capstone project:** Rebuild an Awwwards site from scratch. Use [Website-Blueprints/](Website-Blueprints/) as your spec library.

---

## Track E — AI Engineer

> Goal: ship LLM features that don't embarrass you in prod.

1. **LLM fundamentals** — context windows, sampling, function calling. → [LLM/](LLM/)
2. **Prompt engineering** — structured prompts, evals. → [Prompt-Engineering/](Prompt-Engineering/), [PROMPTS.md](PROMPTS.md)
3. **RAG** — embeddings, vector DBs, chunking. → [AI/](AI/rag.md)
4. **Agents** — tool use, planning, loops. → [Agentic-Coding/](Agentic-Coding/)
5. **MCP** — Model Context Protocol servers. → [MCP/](MCP/)
6. **Safety** — prompt injection, output validation, cost. → [Security/](Security/ai.md)
7. **Evals** — don't ship without them. → [AI/](AI/evals.md)
8. **Cost & latency** — caching, streaming, model routing. → [Performance/](Performance/ai.md)

**Capstone project:** Build a production RAG chatbot over your team's docs. Blueprint: [Website-Blueprints/ai-app.md](Website-Blueprints/ai-app.md).

---

## Track F — AI Agent (You Are the Agent)

You don't "follow" a track. You are the worker. Read [AI_AGENT_GUIDE.md](AI_AGENT_GUIDE.md) — it tells you exactly how to use this repository to plan, build, verify, and ship code without hallucinating.

---

## After Your Track

- Skim [BEST_PRACTICES.md](BEST_PRACTICES.md) and [COMMON_MISTAKES.md](COMMON_MISTAKES.md) — they're cross-cutting.
- Bookmark [CHEATSHEET.md](CHEATSHEET.md) — quick syntax for everything.
- Run every applicable checklist in [Checklists/](Checklists/) before shipping.
- Read [ANTI-PATTERNS.md](ANTI-PATTERNS.md) to know what *not* to do.

---

**Next:** [ROADMAP.md](ROADMAP.md) · [INDEX.md](INDEX.md) · [AI_AGENT_GUIDE.md](AI_AGENT_GUIDE.md)
