# Templates

> Code skeletons to start from. Copy. Customize. Ship.

---

## Purpose

Provide ready-to-use project templates with sensible defaults.

## Prerequisites

- Node.js / Bun installed.

## Learning Outcome

You can scaffold a new project in minutes.

## Related Files

- [Projects/](../Projects/) · [Website-Blueprints/](../Website-Blueprints/) · [EXTERNAL_REPOSITORIES.md](../EXTERNAL_REPOSITORIES.md)

## AI Instructions

When using a template:
1. Copy the template.
2. Update package.json (name, version, repo).
3. Update README.
4. Set up env vars.
5. Run `npm install && npm run dev`.
6. Customize per [ANTI-AI-DESIGN/](../ANTI-AI-DESIGN/).

## Templates

| Template | Stack | Path |
|---|---|---|
| Next.js App (default) | Next.js 15 + TS + Tailwind + shadcn/ui | [_next-app/](./_next-app/) |
| Project Spec | Markdown PLAN.md template | [_project-spec/](./_project-spec/) |
| ADR | Architecture Decision Record | [_adr/](./_adr/) |
| Component Library | React + Tailwind + Storybook | [_component-lib/](./_component-lib/) |
| API Server | Hono + Drizzle + Postgres | [_api-hono/](./_api-hono/) |
| Monorepo | Turborepo + pnpm workspaces | [_monorepo/](./_monorepo/) |

## Quick Start (Next.js)

```bash
# Option 1: Official create-next-app (recommended)
npx create-next-app@latest my-app --typescript --tailwind --app --src-dir --import-alias "@/*"

# Option 2: T3 Stack (Next + tRPC + Prisma + Tailwind + NextAuth)
npx create-t3-app@latest

# Option 3: shadcn/ui
npx shadcn@latest init
```

## What every template should include

- [ ] README.md (how to run).
- [ ] .gitignore.
- [ ] .env.example.
- [ ] .editorconfig.
- [ ] tsconfig.json (strict).
- [ ] ESLint + Prettier (or Biome).
- [ ] Vitest + Testing Library + Playwright configured.
- [ ] CI/CD (GitHub Actions).
- [ ] Pre-commit hooks (Husky + lint-staged).
- [ ] Dockerfile (multi-stage, non-root).
- [ ] Health check endpoint.
- [ ] Error tracking (Sentry) stubbed.
- [ ] Logging (Pino) configured.
- [ ] Env var validation (Zod).
- [ ] LICENSE (MIT).
- [ ] CONTRIBUTING.md.
- [ ] CHANGELOG.md.

---

**Previous:** [Website-Blueprints/](../Website-Blueprints/) · Back to [README.md](../README.md)
