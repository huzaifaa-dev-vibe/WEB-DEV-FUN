# DEPLOYMENT (Overview)

> Ship safely. Roll back fast. Deep coverage in [Deployment/](Deployment/) and provider folders.

---

## Purpose

Get code from your laptop to production safely, repeatably, and reversibly.

## Prerequisites

- Git, basic server knowledge.

## Learning Outcome

You can choose a deployment strategy, implement zero-downtime deploys, and roll back when things break.

## Related Files

- [Deployment/](Deployment/) — strategies
- [Vercel/](Vercel/), [Netlify/](Netlify/), [Cloudflare/](Cloudflare/), [AWS/](AWS/), [Azure/](Azure/), [GCP/](GCP/)
- [Docker/](Docker/), [Kubernetes/](Kubernetes/)
- [CI-CD/](CI-CD/)
- [Checklists/pre-launch.md](Checklists/pre-launch.md)

## AI Instructions

When deploying:
1. Pick provider per [DEPLOYMENT.md#decision-tree](#decision-tree).
2. Set up CI/CD per [CI-CD/](CI-CD/).
3. Configure preview deploys per PR.
4. Configure health checks (`/health`, `/ready`).
5. Configure rollback.
6. Set up monitoring + alerts before deploying.
7. Document the deploy + rollback procedure in the project README.

## Decision Tree

```
Is it a static site or SPA?
├─ Yes → Vercel / Netlify / Cloudflare Pages
└─ No → Is it Next.js / Remix / Astro SSR?
   ├─ Yes → Vercel (best DX) or Netlify or Cloudflare Workers
   └─ No → Is it containerized backend?
      ├─ Yes →
      │   ├─ Small team / simple → Fly.io / Railway / Render
      │   ├─ Need scale / control → AWS ECS / GCP Cloud Run / Azure Container Apps
      │   └─ Complex / multi-service → Kubernetes (EKS/GKE/AKS)
      └─ No → Is it a managed service (Supabase, Firebase, Appwrite)?
         └─ Yes → Use that provider's deploy flow
```

## Strategies

### Rolling
- Replace instances gradually.
- Pros: simple, no downtime.
- Cons: slow; during rollout, two versions serve traffic.

### Blue-Green
- Two environments. Switch traffic.
- Pros: instant switch, instant rollback.
- Cons: 2x resources.

### Canary
- Release to a small % of users. Increase if healthy.
- Pros: limits blast radius.
- Cons: needs traffic routing + monitoring.

### Feature Flags
- Decouple deploy from release.
- Pros: ship dark, turn on gradually.
- Cons: tech debt if flags live forever.

→ [Deployment/strategies.md](Deployment/strategies.md)

## Zero-Downtime Checklist

- [ ] Health check endpoint
- [ ] New version passes health check before traffic
- [ ] Old version kept until new verified
- [ ] DB migrations backward-compatible
- [ ] Static assets versioned (cache-busting)
- [ ] Sessions survive deploy (sticky or stateless)
- [ ] Rollback documented and tested

## Rollback

Rollback must be:
- **Fast** (< 5 min)
- **Tested** (practice in staging)
- **Documented** (runbook)

Database changes complicate rollback. → [PostgreSQL/migrations.md](PostgreSQL/migrations.md) for forward-only migrations.

## Pre-Deploy Checklist

→ [Checklists/pre-launch.md](Checklists/pre-launch.md)

Highlights:
- [ ] All tests pass in CI
- [ ] Lighthouse ≥ 90 (mobile)
- [ ] Security headers set
- [ ] HTTPS + HSTS
- [ ] Env vars in secrets manager (not code)
- [ ] Logs shipping to aggregator
- [ ] Alerts configured
- [ ] On-call rotation set
- [ ] Rollback procedure documented
- [ ] DNS + CDN configured
- [ ] Backups verified

## Provider Quick Picks

| Need | Pick |
|---|---|
| Next.js / React frontend | Vercel |
| Static + serverless functions | Netlify / Cloudflare Pages |
| Edge-first (low latency globally) | Cloudflare Workers |
| Containerized backend, small team | Fly.io / Railway / Render |
| Containerized backend, enterprise | AWS ECS / GCP Cloud Run |
| Complex multi-service | Kubernetes (EKS/GKE) |
| Serverless functions | AWS Lambda / Cloudflare Workers / Vercel Functions |
| Managed Postgres | Supabase / Neon / PlanetScale (MySQL) / RDS |
| Managed Redis | Upstash / Redis Cloud / ElastiCache |
| Managed auth | Clerk / Auth0 / Supabase Auth / Stytch |
| Managed search | Algolia / Meilisearch Cloud / Typesense Cloud |
| Managed files | Cloudflare R2 / AWS S3 / Backblaze B2 |
| Managed email | Resend / Postmark / SendGrid |
| Managed payments | Stripe |

## References

- Vercel docs: https://vercel.com/docs
- Cloudflare docs: https://developers.cloudflare.com/
- Fly.io docs: https://fly.io/docs/
- AWS docs: https://docs.aws.amazon.com/
- Google Cloud docs: https://cloud.google.com/docs

## Further Reading

- *Continuous Delivery* — Jez Humble, David Farley
- *Release It!* — Michael Nygard
- *Site Reliability Engineering* — Google (free)

## Exercises

1. Deploy the same app to Vercel, Netlify, and Cloudflare Pages. Compare.
2. Set up blue-green deploy on Fly.io.
3. Practice rollback. Time yourself.

## Projects

- Build a deploy pipeline with preview environments per PR.
- Set up canary deploy with feature flags (PostHog, LaunchDarkly, or open-source Unleash).

---

**Next:** [Deployment/](Deployment/) · [CI-CD/](CI-CD/) · [Checklists/pre-launch.md](Checklists/pre-launch.md)
