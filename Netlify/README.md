# Netlify

> Static sites + serverless functions. Great DX, Git-based deploys.

---

## Purpose

Deploy static sites and Jamstack apps to Netlify.

## Prerequisites

- A static site or SPA.

## Learning Outcome

You can deploy to Netlify with functions, forms, identity, and analytics.

## Dependencies

- Netlify account.

## Related Files

- [Vercel/](../Vercel/) · [Cloudflare/](../Cloudflare/) · [Deployment/](../Deployment/)

## AI Instructions

When deploying to Netlify:
1. Connect Git repo. Auto-deploys.
2. Preview deploys per PR.
3. Set env vars.
4. Use Netlify Functions for serverless.
5. Use Netlify Forms for form handling.
6. Use `netlify.toml` for config.
7. Custom domains with auto SSL.

## Human Notes

### Deploy
- Connect Git.
- Build command (e.g., `npm run build`).
- Publish directory (e.g., `dist`).
- Auto-deploys on push.

### CLI
```bash
npm i -g netlify-cli
netlify deploy
netlify deploy --prod
netlify env:set DATABASE_URL ...
netlify functions:create
```

### netlify.toml
```toml
[build]
  command = "npm run build"
  publish = "dist"

[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200

[[headers]]
  for = "/*"
  [headers.values]
    X-Frame-Options = "DENY"
```

### Functions
```ts
// netlify/functions/hello.ts
export default async (req: Request) => {
  return new Response(JSON.stringify({ hello: 'world' }), {
    headers: { 'Content-Type': 'application/json' },
  });
};
```
URL: `/.netlify/functions/hello`.

### Forms
Netlify auto-detects HTML forms. Add `data-netlify="true"`.

### Identity
Built-in auth (Magic links, OAuth, etc.).

### Analytics
Privacy-friendly, server-side.

### When to use Netlify
- Static sites / SPAs.
- Marketing sites.
- Docs (with integrations).
- Forms-heavy sites.

### When NOT to use
- Next.js App Router (use Vercel).
- Heavy backend (use Fly.io / AWS).

## Common Mistakes

- ❌ Long functions (timeout).
- ❌ Big deploys (slow).
- ❌ No env var separation.

## Tools

- Netlify docs: https://docs.netlify.com/
- Netlify CLI: https://docs.netlify.com/cli/get-started/

## References

- Netlify: https://www.netlify.com/

## Exercises

1. Deploy a static site.
2. Add a serverless function.
3. Add a form.

## Projects

- Build a marketing site with forms + CMS.

---

**Previous:** [Vercel/](../Vercel/) · **Next:** [Cloudflare/](../Cloudflare/) · **Related:** [Deployment/](../Deployment/)
