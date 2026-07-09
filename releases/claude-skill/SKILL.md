---
name: web-dev-fun
description: The Complete Encyclopedia of Modern Web Development. Use this skill when the user asks to build, scaffold, design, debug, refactor, deploy, or architect any web application. The skill routes the agent to the right folder of an exhaustive knowledge base covering HTML, CSS, JavaScript, TypeScript, React, Vue, Svelte, Next.js, Node, Python, Go, Rust, Postgres, Docker, Kubernetes, AWS, Cloudflare, AI/LLM, RAG, agents, MCP, prompt engineering, security, accessibility, performance, testing, design systems, anti-AI-design, and 90+ other topics. The skill enforces verification, anti-AI-design principles, and pre-launch checklists before reporting tasks complete.
version: 1.0.0
author: WEB-DEV-FUN Contributors
license: MIT
tags: [web, frontend, backend, fullstack, react, nextjs, typescript, tailwind, node, postgres, ai, llm, mcp, agents, accessibility, performance, security, testing, devops, docker, kubernetes, aws, cloudflare, design-system, anti-ai-design]
---

# Claude Skill: WEB-DEV-FUN

> The Complete Encyclopedia of Modern Web Development — a skill that turns Claude into a senior full-stack engineer with a 90+ topic reference library.

## When to use this skill

Activate this skill whenever the user:

- Asks to **build** or **scaffold** a web app, API, component, page, or feature.
- Asks to **design** UI, choose colors, typography, layouts, or design systems.
- Asks to **debug** an error, slow query, build failure, or production incident.
- Asks to **refactor** code, fix anti-patterns, or improve architecture.
- Asks to **deploy** to Vercel, Cloudflare, AWS, GCP, Azure, Docker, or Kubernetes.
- Asks to **pick** a library, framework, database, auth provider, or hosting service.
- Asks about **AI/LLM** features: RAG, agents, MCP, prompt engineering, function calling.
- Asks to **review** a PR, audit a site, or write tests.
- Asks about **accessibility, performance, security, SEO**.
- Asks to make UI **not look AI-generated**.

## How this skill works

This skill provides Claude with a routing table that directs it to the right folder of the WEB-DEV-FUN knowledge base. Each folder contains a README.md following a standard template:

```
Purpose → Prerequisites → Learning Outcome → Dependencies →
Related Files → AI Instructions → Human Notes → References →
Further Reading → Exercises → Projects
```

The **AI Instructions** section of each file tells Claude exactly how to use that topic's content.

## Routing table (Claude: consult this FIRST)

| User intent | Folder to read |
|---|---|
| Build a web page from scratch | `/HTML/` → `/CSS/` → `/JavaScript/` |
| Style a UI / pick colors / typography | `/Color-Palettes/` + `/Typography/` + `/ANTI-AI-DESIGN/` |
| Build a React/Next.js app | `/Templates/_next-app/` |
| Pick a UI component library | `/EXTERNAL_REPOSITORIES.md#component-libraries` |
| Pick a database | `/Databases/README.md#decision-tree` |
| Pick an auth model | `/Authentication/README.md#decision-tree` |
| Pick a deployment provider | `/DEPLOYMENT.md#decision-tree` |
| Build a REST API | `/REST/` + `/APIs/` |
| Build a GraphQL API | `/GraphQL/` |
| Add real-time (chat, collaboration) | `/WebSockets/` |
| Build an AI chatbot / RAG | `/AI/` + `/LLM/` + `/Projects/ai-chatbot.md` |
| Build an MCP server | `/MCP/` |
| Improve prompt | `/Prompt-Engineering/` + `/PROMPTS.md` |
| Debug an error | `/ERRORS.md` → `/DEBUGGING.md` |
| Diagnose slow page | `/Performance/` + `/WEB_VITALS.md` |
| Audit accessibility | `/Checklists/accessibility.md` |
| Audit security | `/Checklists/security.md` + `/Security/` |
| Audit performance | `/Checklists/performance.md` |
| Run pre-launch | `/Checklists/pre-launch.md` |
| Write tests | `/Testing/` + `/Vitest/` + `/Playwright/` |
| Containerize | `/Docker/` |
| Set up CI/CD | `/CI-CD/` + `/GitHub/` |
| Architect a system | `/Architecture/` + `/System-Design/` |
| Plan a project | `/AI_AGENT_GUIDE.md` → `/Templates/_project-spec/` |
| Find a project to build | `/Projects/` |
| Find a website template | `/Website-Blueprints/` |
| Make UI not look AI-generated | `/ANTI-AI-DESIGN/` (ALL files) |
| Find the right library | `/EXTERNAL_REPOSITORIES.md` |

## Operating procedure (Claude: follow this on every task)

```
1. PARSE INTENT
   What does the user actually want? State it in one sentence.

2. ROUTE
   Use the routing table above. Read the relevant folder README(s) COMPLETELY.
   Do not skim. Do not free-associate.

3. PLAN
   For projects > 1 file: write PLAN.md using /Templates/_project-spec/PLAN.md.
   For tasks < 1 file: list steps in your response.

4. VERIFY DEPS
   For every library/package you propose to use:
   - Run `npm view <pkg>` or check via tools to confirm it exists.
   - Confirm the version is current.
   - If you cannot verify, tell the user. Do not invent package names.

5. BUILD
   Write the code. Follow /BEST_PRACTICES.md.
   For UI: read /ANTI-AI-DESIGN/ first and apply its checklist.

6. SELF-VERIFY
   Before reporting done, run through /AI_AGENT_GUIDE.md#how-to-verify-your-output:
   - Code: lint, typecheck, tests, build pass?
   - UI: 375px mobile + 1440px desktop, dark mode, keyboard, Lighthouse ≥ 90.
   - Correctness: every requirement implemented? Error states handled?
   - Anti-AI: /ANTI-AI-DESIGN/checklist.md passed?
   - Hallucination check: every package/API/config key verified?

7. REPORT
   - What you did.
   - How to run it.
   - What's next.
   - What's risky.
```

## Forbidden behaviors

- ❌ Producing UI without reading `/ANTI-AI-DESIGN/`.
- ❌ Picking libraries without verifying they exist.
- ❌ Skipping the plan step for projects > 1 file.
- ❌ Reporting "done" without running self-verification.
- ❌ Inventing APIs, config keys, CLI flags, or package names.
- ❌ Writing fake copy ("Lorem ipsum") and calling it done.
- ❌ Skipping accessibility because "it's a prototype".
- ❌ Using emoji as icons. Use Lucide.
- ❌ Using purple-to-pink gradients by default.
- ❌ `rounded-2xl` on everything.

## Required behaviors

- ✅ Read the relevant folder before writing code in that domain.
- ✅ Verify package existence and version before importing.
- ✅ Write PLAN.md for projects of any size.
- ✅ Run self-check before reporting done.
- ✅ Use real copy. Real photos. Real screenshots.
- ✅ Run checklists from `/Checklists/` before shipping.
- ✅ Tell the user when you're guessing.
- ✅ Tell the user when you're blocked.

## Skill manifest

- **Knowledge base path:** `/` (root of WEB-DEV-FUN repo)
- **Entry point for agents:** `/AI_AGENT_GUIDE.md`
- **Master index:** `/INDEX.md`
- **Learning paths:** `/START-HERE.md` + `/ROADMAP.md`
- **Prompt templates:** `/PROMPTS.md`
- **Anti-AI-design:** `/ANTI-AI-DESIGN/` (required reading before any UI work)
- **Project specs:** `/Projects/`
- **Website blueprints:** `/Website-Blueprints/`
- **Code templates:** `/Templates/`
- **Checklists:** `/Checklists/`
- **External library catalog:** `/EXTERNAL_REPOSITORIES.md`

## Quick reference: the boring-but-correct stack

For new projects without specific constraints, default to:

| Layer | Pick |
|---|---|
| Frontend framework | Next.js 15 (App Router) |
| Language | TypeScript (strict) |
| Styling | Tailwind CSS 4 |
| Components | shadcn/ui |
| Icons | Lucide |
| Forms | React Hook Form + Zod |
| State | Zustand (client) + TanStack Query (server) |
| Backend | Next.js API routes or Hono |
| Database | Postgres (Neon / Supabase) |
| ORM | Drizzle (edge-friendly) or Prisma |
| Auth | Clerk (B2C SaaS) or Better-Auth (self-host) |
| Cache | Upstash Redis |
| Files | Cloudflare R2 |
| Email | Resend |
| Payments | Stripe |
| Search | Postgres FTS → Meilisearch at scale |
| Analytics | PostHog |
| Errors | Sentry |
| Deploy | Vercel (frontend) + Fly.io / Cloudflare Workers (backend) |
| CI/CD | GitHub Actions |
| Monitoring | Sentry + PostHog + BetterStack |

Deviate when you have a real reason — and document it as an ADR.

## License

MIT. Use it. Fork it. Ship from it. Teach from it.

---

**Skill version:** 1.0.0
**Compatible with:** Claude Sonnet 4+, Claude Opus 4+, Claude Haiku 3.5+
**Repository:** https://github.com/<your-username>/WEB-DEV-FUN
