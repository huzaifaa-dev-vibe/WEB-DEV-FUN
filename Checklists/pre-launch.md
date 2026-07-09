# Pre-Launch Checklist

> Run before going live. Treat every unchecked item as a blocker.

---

## Performance
- [ ] Lighthouse mobile ≥ 90 all categories.
- [ ] LCP < 2.5s on critical pages.
- [ ] CLS < 0.1.
- [ ] INP < 200ms.
- [ ] TTFB < 800ms.
- [ ] Bundle < 200KB (gzip) for critical path.
- [ ] Images AVIF/WebP + srcset + lazy.
- [ ] Fonts `font-display: swap` + `preload`.
- [ ] HTTP/2 or HTTP/3 enabled.
- [ ] Brotli compression.
- [ ] CDN configured.
- [ ] Caching headers set.

## Accessibility
- [ ] axe DevTools: 0 issues.
- [ ] Lighthouse a11y ≥ 95.
- [ ] Keyboard nav tested (no mouse).
- [ ] Screen reader test (VoiceOver / NVDA).
- [ ] All images have `alt`.
- [ ] All inputs have `<label>`.
- [ ] Color contrast ≥ 4.5:1.
- [ ] `:focus-visible` visible everywhere.
- [ ] Heading order logical.
- [ ] Skip-to-content link.
- [ ] `prefers-reduced-motion` respected.

## Security
- [ ] HTTPS enforced + HSTS.
- [ ] Security headers (securityheaders.com A+).
- [ ] CSP strict (nonces/hashes).
- [ ] CORS allowlist (no `*` with credentials).
- [ ] All inputs validated.
- [ ] All SQL parameterized.
- [ ] Passwords hashed (bcrypt/argon2).
- [ ] Auth tokens: short TTL + refresh rotation.
- [ ] Rate limiting on auth + write endpoints.
- [ ] CSRF protection (cookie-based auth).
- [ ] No secrets in code or env of client bundle.
- [ ] Dependency audit clean (`npm audit`).
- [ ] WAF configured (for public apps).

## SEO
- [ ] Unique title per page (50–60 chars).
- [ ] Unique meta description per page (150–160).
- [ ] OpenGraph + Twitter Card tags.
- [ ] Canonical URLs.
- [ ] sitemap.xml submitted to Search Console.
- [ ] robots.txt.
- [ ] JSON-LD structured data.
- [ ] All images have `alt`.
- [ ] Mobile-friendly.
- [ ] HTTPS, no mixed content.

## Observability
- [ ] Error tracking (Sentry) installed + tested.
- [ ] Uptime monitoring configured.
- [ ] Alerts configured with runbooks.
- [ ] Logs shipping to aggregator.
- [ ] Metrics dashboard (Grafana / Datadog).
- [ ] Traces (OpenTelemetry).
- [ ] On-call rotation set (even if just you).
- [ ] Status page set up.

## Data
- [ ] Backups verified (DB + user-uploaded files).
- [ ] Restore from backup tested.
- [ ] DB migrations forward-compatible.
- [ ] Connection pooling configured.

## Deployment
- [ ] Preview deploys per PR.
- [ ] Zero-downtime deploy (rolling or blue-green).
- [ ] Health checks (`/health`, `/ready`).
- [ ] Rollback documented + tested.
- [ ] Feature flags for risky changes.
- [ ] Secrets in CI/CD secrets (not in repo).
- [ ] DNS configured.
- [ ] SSL cert installed + auto-renewing.

## UX
- [ ] Empty states designed.
- [ ] Loading states (skeleton > spinner).
- [ ] Error states (with retry).
- [ ] 404 page helpful.
- [ ] 500 page helpful.
- [ ] Form validation messages clear.
- [ ] Mobile UX tested on real device.

## Business
- [ ] Privacy policy published.
- [ ] Terms of service published.
- [ ] Cookie banner (if required).
- [ ] Analytics installed (privacy-respecting).
- [ ] Email templates tested.
- [ ] Payment flow tested end-to-end.
- [ ] Refund/cancel flow tested.

## Anti-AI-Design
- [ ] Run [ANTI-AI-DESIGN/checklist.md](../ANTI-AI-DESIGN/checklist.md).

## Final
- [ ] Soft launch / dogfood with team.
- [ ] Beta launch with friendly users.
- [ ] Feedback channel ready.
- [ ] Announcement ready (blog, social, email).
- [ ] Deploy Mon–Thu morning. Not Friday.

---

**Previous:** [pre-flight.md](pre-flight.md) · **Next:** [accessibility.md](accessibility.md) · Back to [Checklists/](README.md)
