# Codex Agent Configuration — WEB-DEV-FUN

> Drop this file at the root of your project as `AGENTS.md` to give OpenAI Codex (and Codex CLI) instant context about the WEB-DEV-FUN knowledge base and how to use it.

---

## Repository purpose

WEB-DEV-FUN is **The Complete Encyclopedia of Modern Web Development** — a reference manual for both humans and AI coding agents (Codex, Claude, Cursor, Cline, Aider, etc.). It covers 90+ topics: HTML, CSS, JavaScript, TypeScript, React, Vue, Svelte, Next.js, Node, Bun, Deno, Python, Go, Rust, Postgres, MongoDB, Redis, Prisma, Drizzle, Docker, Kubernetes, AWS, Cloudflare, Vercel, AI/LLM, RAG, MCP, agents, prompt engineering, security, accessibility, performance, testing, design systems, anti-AI-design, and more.

## How Codex should use this repository

### Routing table (consult FIRST before writing any code)

| Task | Read |
|---|---|
| Build a web page | `/HTML/`, `/CSS/`, `/JavaScript/` |
| Style UI / pick colors / typography | `/Color-Palettes/`, `/Typography/`, `/ANTI-AI-DESIGN/` |
| Scaffold a Next.js app | `/Templates/_next-app/` |
| Pick a component library | `/EXTERNAL_REPOSITORIES.md#component-libraries` |
| Pick a database | `/Databases/README.md#decision-tree` |
| Pick an auth model | `/Authentication/README.md#decision-tree` |
| Pick a deploy target | `/DEPLOYMENT.md#decision-tree` |
| Build a REST API | `/REST/`, `/APIs/` |
| Build a GraphQL API | `/GraphQL/` |
| Add real-time | `/WebSockets/` |
| Build an AI chatbot / RAG | `/AI/`, `/LLM/`, `/Projects/ai-chatbot.md` |
| Build an MCP server | `/MCP/` |
| Improve a prompt | `/Prompt-Engineering/`, `/PROMPTS.md` |
| Debug an error | `/ERRORS.md` → `/DEBUGGING.md` |
| Diagnose slow page | `/Performance/`, `/WEB_VITALS.md` |
| Audit accessibility | `/Checklists/accessibility.md` |
| Audit security | `/Checklists/security.md`, `/Security/` |
| Run pre-launch | `/Checklists/pre-launch.md` |
| Write tests | `/Testing/`, `/Vitest/`, `/Playwright/` |
| Containerize | `/Docker/` |
| Set up CI/CD | `/CI-CD/`, `/GitHub/` |
| Architect a system | `/Architecture/`, `/System-Design/` |
| Plan a project | `/AI_AGENT_GUIDE.md`, `/Templates/_project-spec/` |
| Make UI not look AI-generated | `/ANTI-AI-DESIGN/` (ALL files) |
| Find a project to build | `/Projects/` |
| Find a website template | `/Website-Blueprints/` |
| Find the right library | `/EXTERNAL_REPOSITORIES.md` |

### Operating procedure

```
1. PARSE INTENT — what does the user actually want?
2. ROUTE — use the routing table; read the folder README completely.
3. PLAN — for projects > 1 file, write PLAN.md from /Templates/_project-spec/.
4. VERIFY DEPS — `npm view <pkg>` or `gh repo view` to confirm. Never invent names.
5. BUILD — write code per /BEST_PRACTICES.md.
6. SELF-VERIFY — run /AI_AGENT_GUIDE.md#how-to-verify-your-output.
7. REPORT — what, how to run, next steps, risks.
```

### Codex project rules (apply to all generated code)

- **Language:** TypeScript (strict, `noUncheckedIndexedAccess: true`).
- **Frontend:** Next.js 15 App Router by default. Server Components unless client needed.
- **Styling:** Tailwind CSS 4. No inline styles. No CSS-in-JS unless asked.
- **Components:** shadcn/ui (Radix + Tailwind). Don't reinvent.
- **Icons:** Lucide. NEVER emoji.
- **Forms:** React Hook Form + Zod.
- **State:** Zustand (client) + TanStack Query (server).
- **DB:** Postgres via Drizzle (edge-friendly) or Prisma (better DX).
- **Auth:** Clerk (B2C SaaS) or Better-Auth (self-host).
- **Validation:** Zod at every boundary. Validate all external input.
- **Errors:** Throw typed errors. Central error middleware. Never silent `catch {}`.
- **Logging:** Pino with request IDs. Never `console.log` in committed code.
- **Tests:** Vitest (unit) + Testing Library (component) + Playwright (E2E).
- **No `any`** without a comment explaining why.
- **No `dangerouslySetInnerHTML`** without DOMPurify.
- **No `eval` / `Function()`** with user input.
- **Conventional Commits:** `feat:`, `fix:`, `chore:`, `docs:`, `refactor:`, `test:`, `perf:`.

### Anti-AI-Design rules (apply to all generated UI)

Before generating any UI, READ `/ANTI-AI-DESIGN/checklist.md`. Apply:

- NO centered hero + 2 CTAs + 3 feature cards. Pick alternative from `/ANTI-AI-DESIGN/hero-alternatives.md`.
- NO purple-to-pink gradient.
- NO `rounded-2xl` on everything. Mix radii.
- NO emoji icons.
- NO lorem ipsum or generic copy. Real copy.
- NO fake testimonials with stock photos.
- NO `fade-in-up` on every section.
- YES one intentional imperfection (slight rotation, asymmetric detail).
- YES real photos / real screenshots / real copy.
- YES `prefers-reduced-motion` respected.
- YES accessibility (keyboard, contrast ≥ 4.5:1, focus-visible, ARIA).

### Verification before reporting "done"

- [ ] `pnpm lint` exits 0.
- [ ] `pnpm typecheck` exits 0.
- [ ] `pnpm test` exits 0.
- [ ] `pnpm build` exits 0.
- [ ] Every imported package verified at the version specified.
- [ ] Every external URL referenced is reachable.
- [ ] Mobile (375px) + Desktop (1440px) verified. No horizontal scroll.
- [ ] Dark mode readable.
- [ ] Keyboard nav works. Focus visible.
- [ ] `/ANTI-AI-DESIGN/checklist.md` passed.
- [ ] `/Checklists/pre-flight.md` passed.

### Forbidden

- Inventing package names, APIs, config keys, CLI flags, or version numbers.
- Reporting "done" without running the self-verification.
- Producing UI without reading `/ANTI-AI-DESIGN/`.
- Silently failing (always report blockers).
- Skipping accessibility because "it's a prototype".

### Required reading order (for new agents)

1. `/AI_AGENT_GUIDE.md` — the contract.
2. `/INDEX.md` — table of contents.
3. `/BEST_PRACTICES.md` — universal rules.
4. `/COMMON_MISTAKES.md` — what to avoid.
5. `/ANTI-AI-DESIGN/README.md` — required for any UI work.
6. The folder README for the specific task domain.

### Boring-but-correct default stack

| Layer | Pick |
|---|---|
| Frontend | Next.js 15 |
| Language | TypeScript (strict) |
| Styling | Tailwind CSS 4 |
| Components | shadcn/ui |
| Icons | Lucide |
| Forms | React Hook Form + Zod |
| State | Zustand + TanStack Query |
| Backend | Next.js API / Hono |
| DB | Postgres (Neon / Supabase) |
| ORM | Drizzle or Prisma |
| Auth | Clerk or Better-Auth |
| Cache | Upstash Redis |
| Files | Cloudflare R2 |
| Email | Resend |
| Payments | Stripe |
| Analytics | PostHog |
| Errors | Sentry |
| Deploy | Vercel + Fly.io / Cloudflare |
| CI/CD | GitHub Actions |

---

**File purpose:** Place at project root as `AGENTS.md`. Codex CLI auto-detects and uses it.
**Repository:** https://github.com/<your-username>/WEB-DEV-FUN
**Version:** 1.0.0
**License:** MIT
