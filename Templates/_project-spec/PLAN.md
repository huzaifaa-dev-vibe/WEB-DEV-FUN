# Project Spec Template

> Copy this file. Fill in. Save as `PLAN.md` in project root.

---

# PLAN — <project name>

## 1. Problem statement
<What user problem does this solve? One paragraph. No tech.>

## 2. Users & personas
<Who uses this? What do they want? What stops them today?>

## 3. Scope (in / out)
- IN:
  - <explicit list>
- OUT:
  - <explicit list>

## 4. Functional requirements
- As a <user>, I can <action>, so that <benefit>.

## 5. Non-functional requirements
- Performance: LCP < ?s, INP < ?ms, p99 latency < ?ms.
- Scale: <? users, ? RPS, ? data volume>.
- Security: <auth model, threat model summary>.
- Accessibility: WCAG ??
- Browser support: <matrix>.

## 6. Tech stack (with verification)
| Layer | Choice | Verified | Why |
|---|---|---|---|
| Frontend | Next.js 15 | ✅ | App Router, RSC |
| Backend | (Next.js API / Hono / etc.) | | |
| DB | Postgres (Neon) | ✅ | Relational, JSONB |
| ORM | Drizzle | ✅ | TS-first, edge-friendly |
| Auth | Clerk / Better-Auth / NextAuth | | |
| Deploy | Vercel / Cloudflare / Fly.io | | |
| Monitoring | Sentry + PostHog | | |

## 7. Architecture
<ASCII diagram + 1 paragraph explaining data flow.>

## 8. Data model
<Tables/collections with fields, types, indexes, relationships.>

## 9. Folder structure
<Tree with one-line purpose per top-level folder.>

## 10. Rendering strategy
<Per-route table: SSR / SSG / ISR / CSR / streaming.>

## 11. Auth model
<Flow diagram + token storage + refresh strategy.>

## 12. Testing strategy
<Unit / integration / E2E split. Coverage targets.>

## 13. Deployment
<Provider, env vars, secrets, CI/CD pipeline.>

## 14. Observability
<Logs, metrics, traces, alerts, dashboards.>

## 15. Risks
<Top 5 risks + mitigation.>

## 16. Milestones
M1 → M2 → ... with acceptance criteria.

## 17. Open questions
<What you need the human to decide.>

---

**Back to:** [Templates/](README.md) · [AI_AGENT_GUIDE.md](../../AI_AGENT_GUIDE.md)
