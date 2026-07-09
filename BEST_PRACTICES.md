# BEST PRACTICES

> Cross-cutting rules that apply to every project, every stack, every team. Read once. Re-read every quarter.

This file is the canonical "always do this" list. It is intentionally short — each rule is a one-liner with a link to the deeper folder where relevant.

---

## Universal Engineering Rules

1. **Make it work, make it right, make it fast — in that order.** Don't optimize prematurely. Don't ship broken.
2. **Boring tech wins.** Choose proven tools for the 80% case. Save novelty for the 20% that actually needs it. → [EXTERNAL_REPOSITORIES.md](EXTERNAL_REPOSITORIES.md)
3. **Delete code aggressively.** The best code is no code. The second best is code you deleted.
4. **Symptoms vs. root cause.** Always fix root cause. Band-aids compound. → [DEBUGGING.md](DEBUGGING.md)
5. **Beware the bicycle shed.** Spend your energy on the hard/important decisions, not the easy/visible ones.
6. **Code is read 10x more than written.** Optimize for the reader.
7. **Naming is the hardest part.** Spend more time on names than you think you should. → [Clean-Code/](Clean-Code/)
8. **Tests are documentation that runs.** If you can't test it, you don't understand it. → [Testing/](Testing/)
9. **Logs are for debugging.** Metrics are for alerting. Traces are for understanding. Don't confuse them. → [Logging/](Logging/), [Monitoring/](Monitoring/)
10. **Everything fails.** Design for failure from day one. → [System-Design/](System-Design/)

---

## Frontend Best Practices

→ See [CSS/best-practices.md](CSS/best-practices.md), [JavaScript/best-practices.md](JavaScript/best-practices.md), [Accessibility/](Accessibility/)

1. **Mobile-first.** Always. → [Responsive-Design/](Responsive-Design/)
2. **Progressive enhancement** for critical flows — the page should work without JS for the first paint.
3. **Type everything** in TypeScript. No `any` without a comment explaining why.
4. **Validate at the boundary.** Runtime validation (Zod, Valibot) on every external input — API responses, form input, URL params.
5. **Co-locate state with the component that owns it.** Lift only when needed.
6. **Don't reinvent `<button>`.** Use semantic HTML first, then enhance. → [HTML/](HTML/)
7. **Images: `width`, `height`, `alt`, `loading="lazy"`, `srcset`.** Always. → [Performance/](Performance/)
8. **Don't ship `console.log`.** Use a real logger. Strip them in production.
9. **Bundle size is a budget.** Set it. Enforce it in CI. → [Performance/budgets.md](Performance/budgets.md)
10. **No layout shift.** Reserve space for images, ads, embeds. → [WEB_VITALS.md](WEB_VITALS.md)

---

## Backend Best Practices

→ See [Backend/](Backend/), [APIs/](APIs/), [Security/](Security/)

1. **Validate input at the edge.** Trust nothing from the client.
2. **Idempotency keys** for any mutation that could be retried (payments, sends). → [APIs/idempotency.md](APIs/idempotency.md)
3. **Use the right status code.** Don't `200` everything. → [REST/status-codes.md](REST/status-codes.md)
4. **Database queries are not free.** Profile them. Watch for N+1. → [ORM/n-plus-1.md](ORM/n-plus-1.md)
5. **Transactions for multi-step writes.** Always.
6. **Don't trust the client's clock.** Don't trust the client's identity. Don't trust the client's anything.
7. **Rate limit every public endpoint.** → [Security/rate-limiting.md](Security/rate-limiting.md)
8. **Structured logs with a request ID.** Correlate across services. → [Logging/](Logging/)
9. **Secrets in env vars (or a vault), never in code, never in client bundles.** → [Security/secrets.md](Security/secrets.md)
10. **Migrations are forward-only in production.** Plan backward-compat. → [PostgreSQL/migrations.md](PostgreSQL/migrations.md)

---

## Design & UI Best Practices

→ See [ANTI-AI-DESIGN/](ANTI-AI-DESIGN/), [UI/](UI/), [UX/](UX/)

1. **Don't center everything.** Asymmetry creates hierarchy.
2. **One typeface, three weights, six sizes.** Start there. → [Typography/](Typography/)
3. **Pick a palette with intent.** Don't reach for purple-pink by default. → [Color-Palettes/](Color-Palettes/)
4. **Whitespace is content.** Use it generously.
5. **Animation should explain, not decorate.** → [Animations/](Animations/)
6. **Real copy beats lorem ipsum.** Always.
7. **Real photos beat stock photos.** Always. (Or no photos at all.)
8. **Don't fake testimonials.** Either get real ones or omit the section.
9. **Test on a real phone, not just DevTools.** → [Responsive-Design/](Responsive-Design/)
10. **Run the ANTI-AI-DESIGN checklist before shipping any UI.** → [ANTI-AI-DESIGN/checklist.md](ANTI-AI-DESIGN/checklist.md)

---

## Security Best Practices

→ See [Security/](Security/), [SECURITY.md](SECURITY.md)

1. **OWASP Top 10.** Know them. Audit for them. → [Security/owasp.md](Security/owasp.md)
2. **HTTPS everywhere.** HSTS. No mixed content.
3. **CSP headers.** Strict. → [Security/headers.md](Security/headers.md)
4. **Hash passwords** with bcrypt/argon2. Never store plaintext. Never MD5.
5. **JWTs**: short TTL, refresh tokens, rotate on use. Don't store in localStorage if you can avoid it.
6. **SQL parameterization.** Always. No string concatenation. → [Security/sql-injection.md](Security/sql-injection.md)
7. **CSRF tokens** for cookie-based auth. → [Security/csrf.md](Security/csrf.md)
8. **CORS allowlist.** Never `*` for credentialed requests.
9. **Secret rotation.** Plan for it before you need it.
10. **Threat model** every new feature. → [Security/threat-modeling.md](Security/threat-modeling.md)

---

## Performance Best Practices

→ See [Performance/](Performance/), [WEB_VITALS.md](WEB_VITALS.md)

1. **Measure first.** Lighthouse, WebPageTest, RUM.
2. **Targets**: LCP < 2.5s, CLS < 0.1, INP < 200ms, TTFB < 800ms.
3. **Ship less JS.** The fastest code is the code you didn't ship.
4. **Lazy-load below the fold.** Routes, images, components.
5. **Cache aggressively.** HTTP cache, CDN, service worker. → [Performance/caching.md](Performance/caching.md)
6. **Image format**: AVIF > WebP > JPEG. Always `srcset`.
7. **Fonts**: `font-display: swap`, subset to the languages you use, `preload` the critical one.
8. **Preconnect** to critical origins.
9. **Avoid layout thrash.** Batch DOM reads/writes.
10. **Profile in production.** DevTools lies about prod perf.

---

## Testing Best Practices

→ See [Testing/](Testing/), [TESTING.md](TESTING.md)

1. **Test pyramid.** Lots of unit, some integration, few E2E. → [Testing/pyramid.md](Testing/pyramid.md)
2. **Test behavior, not implementation.** Refactoring shouldn't break tests.
3. **One assertion per test** (mostly). Easier to debug.
4. **Test data should be realistic.** Not "test1", "foo", "bar".
5. **No sleeps in tests.** Use proper async waits.
6. **Flaky tests get fixed or quarantined.** Never ignored.
7. **Coverage is a floor, not a target.** 70% meaningfully covered > 100% line coverage of garbage.
8. **E2E for critical paths only.** They're slow and flaky.
9. **Snapshot tests for truly static output.** Not for components with state.
10. **Test in CI on every PR.** Block merge on regressions.

---

## Git & Collaboration

→ See [Git/](Git/), [CONTRIBUTING.md](CONTRIBUTING.md)

1. **Small PRs.** < 400 lines diff when possible.
2. **One concern per PR.** Don't mix feature + refactor + dep bump.
3. **Conventional Commits.** `feat:`, `fix:`, `chore:`, `docs:`, `refactor:`, `test:`, `perf:`.
4. **Rebase, don't merge** your feature branch onto main (unless you need the audit trail).
5. **Code review is mandatory.** Even for the founder. Even for the staff eng.
6. **Review the test, not just the code.** Does it actually test the behavior?
7. **Describe the WHY in the PR description**, not the WHAT (the diff shows what).
8. **Don't push to main.** No, not "just this once".
9. **Use `pre-commit` hooks** for lint/format. → [Git/hooks.md](Git/hooks.md)
10. **Tag releases** with semver. → [Git/tagging.md](Git/tagging.md)

---

## Deployment & Operations

→ See [Deployment/](DEPLOYMENT.md), [CI-CD/](CI-CD/), [Monitoring/](Monitoring/)

1. **Preview deploys per PR.** Always. → [Vercel/](Vercel/), [Netlify/](Netlify/)
2. **Zero-downtime deploys.** Rolling or blue-green. → [Deployment/](DEPLOYMENT.md#strategies)
3. **Health checks.** `/health` (liveness), `/ready` (readiness).
4. **Rollback is a button.** Practice it. → [Deployment/rollback.md](Deployment/rollback.md)
5. **Feature flags** for risky changes. → [Deployment/feature-flags.md](Deployment/feature-flags.md)
6. **Secrets in CI/CD secrets, not in the repo.** Rotate them.
7. **Set up alerts before you need them.** Page on user-facing symptoms. → [Monitoring/alerting.md](Monitoring/alerting.md)
8. **Dashboards for SLOs, not for vanity.** → [Monitoring/dashboards.md](Monitoring/dashboards.md)
9. **Runbooks for every alert.** → [Monitoring/runbooks.md](Monitoring/runbooks.md)
10. **Post-mortems for every incident.** Blameless. Action items tracked. → [Checklists/post-mortem.md](Checklists/post-mortem.md)

---

## AI Engineering Best Practices

→ See [AI/](AI/), [LLM/](LLM/), [Prompt-Engineering/](Prompt-Engineering/)

1. **Eval before you ship.** No evals = no idea if you regressed. → [AI/evals.md](AI/evals.md)
2. **Stream tokens.** Users hate waiting 10s for a response.
3. **Cache aggressively.** Same prompt → same response (within TTL).
4. **Cost-monitor every endpoint.** LLMs can bankrupt you. → [Performance/ai-cost.md](Performance/ai-cost.md)
5. **Validate LLM output** with a schema (Zod, JSON Schema). Never trust raw output.
6. **Rate-limit per user.** LLM abuse is real.
7. **Prompt injection is a real threat.** Sanitize user content going into prompts. → [Security/ai.md](Security/ai.md)
8. **Use the smallest model that works.** Don't use GPT-4 when GPT-4-mini suffices.
9. **Log every prompt + response** (with PII redaction) for debugging and evals.
10. **Have a fallback** when the LLM is down or rate-limited.

---

## Documentation Best Practices

1. **README answers "what is this and how do I run it?"** in 30 seconds.
2. **Architecture Decision Records (ADRs)** for every non-trivial decision. → [Architecture/adrs.md](Architecture/adrs.md)
3. **Comment the WHY, not the WHAT.** Code shows what; comments explain why.
4. **Keep docs next to the code.** Drift kills distant docs.
5. **Update docs in the same PR as the code change.** No "I'll do it later".
6. **Diagrams are docs.** Version them. → [Architecture/diagrams.md](Architecture/diagrams.md)
7. **Examples should run.** Test them in CI.
8. **Glossary** for project-specific terms. Reduces confusion.
9. **CHANGELOG** for user-facing changes. → [CHANGELOG.md](CHANGELOG.md)
10. **Delete outdated docs.** Stale docs are worse than no docs.

---

## Team & Process

1. **Async by default.** Write things down.
2. **Decisions in writing.** Meetings produce notes, not decisions.
3. **RFCs for big changes.** → [Architecture/rfcs.md](Architecture/rfcs.md)
4. **Onboarding doc.** Day-1 to first-PR checklist.
5. **Weekly tech-debt time.** Don't let it accumulate.
6. **Quarterly roadmap review.** Adjust based on reality.
7. **Pair on hard problems.** Don't hero.
8. **Skip-level 1:1s.** Catch problems early.
9. **Celebrate good work.** Out loud.
10. **Post-mortems are blameless.** → [Checklists/post-mortem.md](Checklists/post-mortem.md)

---

**Next:** [COMMON_MISTAKES.md](COMMON_MISTAKES.md) · [ANTI-PATTERNS.md](ANTI-PATTERNS.md) · [Checklists/](Checklists/)
