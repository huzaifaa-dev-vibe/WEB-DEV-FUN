# CI/CD

> Automate. Every commit. Test, build, deploy.

---

## Purpose

Set up continuous integration and continuous deployment.

## Prerequisites

- [Git/](../Git/), [Testing/](../Testing/), [Docker/](../Docker/).

## Learning Outcome

You can build a CI/CD pipeline that ships safely.

## Dependencies

- A CI/CD platform.

## Related Files

- [Git/](../Git/) · [GitHub/](../GitHub/) · [Docker/](../Docker/) · [Testing/](../Testing/) · [Deployment/](../Deployment/)

## AI Instructions

When setting up CI/CD:
1. **Lint + typecheck + test on every PR.**
2. **Build + deploy on main.**
3. **Preview deploys per PR.**
4. **Cache deps** (npm, pnpm, Docker layers).
5. **Pin action versions** (SHA preferred).
6. **Secrets in CI secrets, not code.**
7. **Fail fast** (parallel jobs).
8. **Notify on failure** (Slack, email).

## Human Notes

### GitHub Actions example
```yaml
# .github/workflows/ci.yml
name: CI

on:
  push:
    branches: [main]
  pull_request:

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: npm
      - run: npm ci
      - run: npm run lint
      - run: npm run typecheck
      - run: npm run test:unit
      - run: npm run test:e2e

  build:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: npm
      - run: npm ci
      - run: npm run build
      - uses: actions/upload-artifact@v4
        with:
          name: build
          path: dist

  deploy:
    needs: build
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    environment: production
    steps:
      - uses: actions/checkout@v4
      - uses: amondnet/vercel-action@v25
        with:
          vercel-token: ${{ secrets.VERCEL_TOKEN }}
          vercel-org-id: ${{ secrets.VERCEL_ORG_ID }}
          vercel-project-id: ${{ secrets.VERCEL_PROJECT_ID }}
          vercel-args: '--prod'
```

### CI best practices
- **Fail fast**: parallel jobs, fail on first error.
- **Cache**: deps + build artifacts + Docker layers.
- **Pin versions**: SHA for actions, exact versions for deps.
- **Secrets**: never log, never echo, rotate.
- **Concurrency**: cancel old runs on same branch.
- **Matrix**: test multiple Node versions if you support them.
- **Timebox**: jobs should complete in <10 min.

### CD best practices
- **Preview deploys** per PR.
- **Auto-deploy** main to staging.
- **Manual approval** for prod.
- **Canary** for risky changes.
- **Rollback** in one click (or one command).
- **Feature flags** to decouple deploy from release.

### Pipeline stages
1. **Lint** — code style.
2. **Typecheck** — types.
3. **Unit tests** — fast.
4. **Integration tests** — DB, etc.
5. **Build** — compile/bundle.
6. **E2E tests** — slow, critical paths.
7. **Security scan** — Snyk, Trivy.
8. **Deploy** — staging → prod.

### Tools
- **GitHub Actions** — default for GitHub repos.
- **GitLab CI** — for GitLab repos.
- **CircleCI** — alternative.
- **Buildkite** — hybrid (your runners).
- **Jenkins** — enterprise legacy.
- **Drone** — open source.
- **Woodpecker** — open source.

### Local CI testing
- `act` — run GitHub Actions locally.
- Docker-based.

### DORA metrics
- **Deployment frequency** — how often you deploy.
- **Lead time for changes** — commit to deploy.
- **Change failure rate** — % of deploys that fail.
- **Time to restore** — incident to recovery.

Elite teams: deploy multiple times/day, <1 hour lead time, <15% failure rate, <1 hour recovery.

## Common Mistakes

- ❌ Long pipelines (>15 min).
- ❌ No caching.
- ❌ Manual deploy steps.
- ❌ No preview environments.
- ❌ Secrets in code.
- ❌ `latest` tags in actions.
- ❌ No rollback.
- ❌ Tests that depend on order.
- ❌ Flaky tests ignored.

## Tools

- GitHub Actions: https://docs.github.com/actions
- GitLab CI: https://docs.gitlab.com/ee/ci/
- CircleCI: https://circleci.com/
- Buildkite: https://buildkite.com/
- act (local): https://github.com/nektos/act

## References

- GitHub Actions docs: https://docs.github.com/actions
- DORA: https://dora.dev/

## Further Reading

- *Continuous Delivery* — Jez Humble, David Farley
- *Accelerate* — Forsgren, Humble, Kim

## Exercises

1. Set up CI for a project (lint, test, build).
2. Add preview deploys per PR.
3. Add CD to production with manual approval.

## Projects

- Build a CI/CD pipeline with canary deploys + automatic rollback.

---

**Previous:** [Kubernetes/](../Kubernetes/) · **Next:** [Git/](../Git/) · **Related:** [Deployment/](../Deployment/)
