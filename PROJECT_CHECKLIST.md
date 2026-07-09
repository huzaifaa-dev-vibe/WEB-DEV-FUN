# PROJECT CHECKLIST

> The single checklist to run for every project. Cross-references the deeper checklists in [Checklists/](Checklists/).

---

## Purpose

Make sure you don't forget the things that bite you in production. Run this checklist at project start, mid-project, and pre-launch.

## Prerequisites

- A project you're starting or running.

## Learning Outcome

You can confidently say "we didn't forget anything major".

## Related Files

- [Checklists/](Checklists/) — every checklist, deep
- [BEST_PRACTICES.md](BEST_PRACTICES.md)
- [COMMON_MISTAKES.md](COMMON_MISTAKES.md)
- [ANTI-PATTERNS.md](ANTI-PATTERNS.md)

## AI Instructions

When starting a project, run the **Setup** section. Mid-project, run **Ongoing**. Before launch, run **Pre-Launch**. After launch, run **Post-Launch**. Treat every unchecked item as a blocker.

---

## Setup (Day 0–1)

- [ ] Problem statement written (1 paragraph, no tech).
- [ ] Users & personas identified.
- [ ] Scope (IN / OUT) explicitly listed.
- [ ] Functional requirements written as user stories.
- [ ] Non-functional requirements (perf, scale, security, a11y) quantified.
- [ ] Tech stack chosen, every choice verified (`npm view` / `gh repo view`).
- [ ] Architecture diagram drawn.
- [ ] Data model sketched.
- [ ] Folder structure decided. → [Templates/](Templates/)
- [ ] Rendering strategy per route decided.
- [ ] Auth model decided.
- [ ] Testing strategy decided.
- [ ] Deployment provider chosen.
- [ ] Observability plan (logs, metrics, traces, alerts).
- [ ] Risks listed with mitigations.
- [ ] Milestones with acceptance criteria.
- [ ] PLAN.md written and reviewed.
- [ ] Repo created with README, LICENSE, .gitignore, .editorconfig.
- [ ] CI/CD pipeline stubbed (lint, typecheck, test, build).
- [ ] Pre-commit hooks (lint, format).
- [ ] Branch protection on main.
- [ ] Secrets strategy decided (env vars, vault).
- [ ] Issue tracker set up.
- [ ] Communication channels (Slack/Discord) set up.

## Ongoing (Every PR)

- [ ] PR describes problem + solution + how to test.
- [ ] PR < 400 lines diff (or justified).
- [ ] One concern per PR.
- [ ] Conventional commit messages.
- [ ] Tests added for new behavior.
- [ ] Lint + typecheck + tests pass in CI.
- [ ] Preview deploy generated.
- [ ] Code reviewed by at least one other human.
- [ ] No secrets in code.
- [ ] No `console.log` in production code.
- [ ] No `any` in TS without a comment.
- [ ] No new dependencies without justification.
- [ ] Documentation updated.
- [ ] Accessibility considered.
- [ ] Performance considered (bundle size, query count).
- [ ] Security considered (input validation, authz).
- [ ] Mobile + desktop verified (or noted as not yet).

## Pre-Launch (Week of)

- [ ] [Checklists/pre-flight.md](Checklists/pre-flight.md) run.
- [ ] [Checklists/pre-launch.md](Checklists/pre-launch.md) run.
- [ ] Lighthouse ≥ 90 (mobile) on critical pages.
- [ ] Core Web Vitals in spec (LCP, CLS, INP).
- [ ] WCAG 2.2 AA audit passed (axe + manual).
- [ ] Security headers verified (securityheaders.com A+).
- [ ] HTTPS + HSTS verified.
- [ ] CORS allowlist verified.
- [ ] Rate limiting on auth + write endpoints.
- [ ] All inputs validated (Zod/Valibot).
- [ ] All SQL parameterized.
- [ ] Passwords hashed (bcrypt/argon2).
- [ ] JWT TTL short, refresh rotation.
- [ ] CSRF protection (if cookie-based).
- [ ] Dependency audit clean (`npm audit`, Snyk).
- [ ] No PII in logs.
- [ ] Error tracking (Sentry) installed + tested.
- [ ] Uptime monitoring configured.
- [ ] Alerts configured with runbooks.
- [ ] On-call rotation set (even if just you).
- [ ] Backups verified (DB + user-uploaded files).
- [ ] Restore from backup tested.
- [ ] Rollback documented and tested.
- [ ] DNS configured.
- [ ] CDN configured.
- [ ] SSL cert installed and auto-renewing.
- [ ] Status page set up.
- [ ] Privacy policy + terms of service published.
- [ ] Cookie banner (if applicable / required).
- [ ] Analytics installed (with privacy config).
- [ ] SEO basics: sitemap.xml, robots.txt, OG cards, schema.
- [ ] 404 page exists and is helpful.
- [ ] 500 page exists and is helpful.
- [ ] Empty states designed.
- [ ] Loading states designed.
- [ ] Error states designed.
- [ ] Email templates tested (signup, reset, etc.).
- [ ] Payment flow tested end-to-end (if applicable).
- [ ] Refund/cancel flow tested.
- [ ] Load test run (k6 / Artillery).
- [ ] Soak test run (long-running).
- [ ] Chaos test (kill a service, see what happens).
- [ ] Runbook for top 5 incidents written.
- [ ] Soft launch / dogfood with team.
- [ ] Beta launch with friendly users.
- [ ] Feedback channel for users.
- [ ] Announcement ready (blog, social, email).

## Launch Day

- [ ] Deploy in the morning (Mon–Thu).
- [ ] Team available for 4 hours after deploy.
- [ ] Dashboard open (errors, latency, traffic).
- [ ] Someone watching logs.
- [ ] Pre-written "all clear" / "rolling back" / "we have an issue" templates ready.
- [ ] If anything goes wrong: rollback > fix-forward. Don't be a hero.

## Post-Launch (Week 1)

- [ ] Daily error review.
- [ ] Daily perf review (LCP, INP).
- [ ] Daily user feedback review.
- [ ] User interviews scheduled.
- [ ] Analytics reviewed.
- [ ] Post-mortem on any incidents.
- [ ] Plan for v1.1 (top 3 issues from launch).
- [ ] Document what went well / what didn't.

## Quarterly

- [ ] Dependency audit + updates.
- [ ] Security audit (OWASP Top 10).
- [ ] Performance audit.
- [ ] Accessibility audit.
- [ ] Backup restore drill.
- [ ] Disaster recovery drill.
- [ ] Tech debt review.
- [ ] Architecture review (ADRs up to date?).
- [ ] On-call rotation review.
- [ ] Runbook review.

## End of Project

- [ ] Post-mortem written.
- [ ] Lessons learned shared.
- [ ] Code archived or open-sourced.
- [ ] DNS / domains renewed or released.
- [ ] Third-party services cancelled.
- [ ] Data archived or deleted per policy.
- [ ] Team recognized.

---

**When in doubt, check more boxes.** The cost of one missed check is often days of firefighting.

---

**Next:** [Checklists/](Checklists/) · [BEST_PRACTICES.md](BEST_PRACTICES.md) · [AI_AGENT_GUIDE.md](AI_AGENT_GUIDE.md)
