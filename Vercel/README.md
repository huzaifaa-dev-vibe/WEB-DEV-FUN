# Vercel

> The platform for frontend frameworks. Best Next.js DX.

---

## Purpose

Deploy Next.js, React, and other frontend frameworks to Vercel.

## Prerequisites

- A Next.js or static site.

## Learning Outcome

You can deploy to Vercel with CI/CD, env vars, domains, edge functions.

## Dependencies

- A Vercel account.

## Related Files

- [Deployment/](../Deployment/) · [Netlify/](../Netlify/) · [Cloudflare/](../Cloudflare/) · [AWS/](../AWS/) · [CI-CD/](../CI-CD/)

## AI Instructions

When deploying to Vercel:
1. Connect GitHub repo. Auto-deploys on push.
2. Preview deploys per PR.
3. Set env vars per environment (Preview / Production).
4. Use Edge Functions for global low-latency.
5. Use Vercel Postgres / KV / Blob / Edge Config for managed services.
6. Use `vercel.json` for config.
7. Custom domains with auto-renewing SSL.

## Human Notes

### Deploy
- Connect GitHub repo.
- Auto-deploys on push to main.
- Preview URL per PR.
- Production deploy on merge to main.

### CLI
```bash
npm i -g vercel
vercel         # deploy preview
vercel --prod  # deploy production
vercel env add DATABASE_URL
vercel logs
vercel domains add myapp.com
```

### vercel.json
```json
{
  "framework": "nextjs",
  "regions": ["iad1", "sfo1"],
  "headers": [
    { "source": "/(.*)", "headers": [{ "key": "X-Frame-Options", "value": "DENY" }] }
  ],
  "redirects": [{ "source": "/old", "destination": "/new", "permanent": true }],
  "rewrites": [{ "source": "/api/(.*)", "destination": "https://api.example.com/$1" }]
}
```

### Edge Functions
- Run on Edge runtime (V8 isolates).
- Global low latency.
- Limited APIs (no Node fs, etc.).

### Vercel managed services
- **Vercel Postgres** (serverless Postgres, powered by Neon).
- **Vercel KV** (Redis).
- **Vercel Blob** (file storage).
- **Vercel Edge Config** (global config).
- **Vercel Analytics** + **Speed Insights**.

### Pricing
- Hobby: free for personal non-commercial.
- Pro: $20/seat/month for teams.
- Enterprise: custom.

### When to use Vercel
- Next.js app.
- Static sites.
- Apps that need preview deploys.
- Frontend-focused teams.

### When NOT to use
- Heavy backend (use Fly.io / AWS / Render).
- Cost-sensitive at scale (Vercel gets expensive).
- Long-running tasks (use a queue + worker elsewhere).

## Common Mistakes

- ❌ Long-running functions (timeout).
- ❌ Big bundles (slower cold starts).
- ❌ Not using preview deploys.
- ❌ Secrets in client code.
- ❌ No env var separation.

## Tools

- Vercel docs: https://vercel.com/docs
- Vercel CLI: https://vercel.com/docs/cli

## References

- Vercel: https://vercel.com/

## Exercises

1. Deploy a Next.js app to Vercel.
2. Set up custom domain.
3. Use Edge Functions.

## Projects

- Build a full-stack app on Vercel (Next.js + Postgres + Auth).

---

**Previous:** [Cloud/](../Cloud/) · **Next:** [Netlify/](../Netlify/) · **Related:** [Deployment/](../Deployment/)
