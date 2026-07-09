# Deployment

> Ship safely. Roll back fast.

---

## Purpose

Pick a deployment strategy, implement zero-downtime, monitor, roll back.

## Prerequisites

- [Git/](../Git/), [Backend/](../Backend/).

## Learning Outcome

You can deploy an app safely and roll back when things break.

## Dependencies

- A hosting provider.

## Related Files

- [DEPLOYMENT.md](../DEPLOYMENT.md) · [Docker/](../Docker/) · [Kubernetes/](../Kubernetes/) · [CI-CD/](../CI-CD/) · [Vercel/](../Vercel/) · [Cloudflare/](../Cloudflare/) · [AWS/](../AWS/) · [Checklists/pre-launch.md](../Checklists/pre-launch.md)

## AI Instructions

When deploying:
1. Pick provider per decision tree in [DEPLOYMENT.md](../DEPLOYMENT.md).
2. CI/CD per [CI-CD/](../CI-CD/).
3. Preview deploys per PR.
4. Health checks (`/health`, `/ready`).
5. Rollback plan documented + tested.
6. Monitoring + alerts before deploying.
7. Deploy Mon–Thu morning. Not Friday.

## Human Notes

→ See [DEPLOYMENT.md](../DEPLOYMENT.md) for the full overview.

### Strategies
- Rolling.
- Blue-green.
- Canary.
- Feature flags.

### Health checks
- `/health` — liveness.
- `/ready` — readiness.

### Graceful shutdown
- SIGTERM → stop accepting → finish in-flight → close DB → exit.

### Rollback
- Must be tested.
- Must be documented.
- DB migrations complicate (forward-only).

### Zero downtime checklist
→ [DEPLOYMENT.md#zero-downtime-checklist](../DEPLOYMENT.md)

## Tools

→ See provider folders: [Vercel/](../Vercel/), [Netlify/](../Netlify/), [Cloudflare/](../Cloudflare/), [AWS/](../AWS/), [Azure/](../Azure/), [GCP/](../GCP/).

## References

- 12-factor app: https://12factor.net/
- Google SRE book (free)

## Exercises

1. Deploy same app to Vercel + Cloudflare Pages. Compare.
2. Set up blue-green deploy.
3. Practice rollback.

## Projects

- Build a CI/CD pipeline with preview deploys.

---

**Previous:** [ORM/](../ORM/) · **Next:** [Docker/](../Docker/) · **Related:** [CI-CD/](../CI-CD/)
