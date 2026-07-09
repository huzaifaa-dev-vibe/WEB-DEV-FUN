# Next.js App Template (Reference)

> Recommended starting point for new Next.js apps.

## Quick start

```bash
# Recommended: official create-next-app
npx create-next-app@latest my-app \
  --typescript \
  --tailwind \
  --app \
  --src-dir \
  --import-alias "@/*" \
  --use-pnpm

cd my-app

# Add shadcn/ui
npx shadcn@latest init

# Add common deps
pnpm add zod react-hook-form @hookform/resolvers
pnpm add @tanstack/react-query
pnpm add lucide-react
pnpm add -D vitest @testing-library/react @testing-library/jest-dom jsdom
pnpm add -D @playwright/test
pnpm add -D prettier eslint-config-prettier
```

## Recommended structure

```
my-app/
├── app/
│   ├── (auth)/
│   │   ├── login/page.tsx
│   │   └── signup/page.tsx
│   ├── (dashboard)/
│   │   ├── layout.tsx
│   │   └── page.tsx
│   ├── api/
│   ├── layout.tsx
│   ├── page.tsx
│   ├── robots.ts
│   ├── sitemap.ts
│   └── globals.css
├── components/
│   ├── ui/                  # shadcn/ui components
│   └── ...
├── lib/
│   ├── db.ts
│   ├── auth.ts
│   ├── validations.ts       # Zod schemas
│   └── utils.ts
├── public/
├── e2e/                     # Playwright
├── .env.example
├── .env.local
├── next.config.ts
├── tailwind.config.ts
├── tsconfig.json
├── package.json
└── README.md
```

## tsconfig.json (strict)

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "lib": ["dom", "dom.iterable", "esnext"],
    "allowJs": true,
    "skipLibCheck": true,
    "strict": true,
    "noEmit": true,
    "esModuleInterop": true,
    "module": "esnext",
    "moduleResolution": "bundler",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "jsx": "preserve",
    "incremental": true,
    "plugins": [{ "name": "next" }],
    "paths": { "@/*": ["./src/*"] },
    "noUncheckedIndexedAccess": true
  },
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx", ".next/types/**/*.ts"],
  "exclude": ["node_modules"]
}
```

## .env.example

```
# App
NEXT_PUBLIC_APP_URL=http://localhost:3000

# DB
DATABASE_URL=postgres://user:pass@localhost:5432/myapp

# Auth
AUTH_SECRET=replace-me
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=
CLERK_SECRET_KEY=

# Analytics
NEXT_PUBLIC_POSTHOG_KEY=
NEXT_PUBLIC_POSTHOG_HOST=https://us.i.posthog.com

# Error tracking
SENTRY_DSN=

# Email
RESEND_API_KEY=

# File storage
R2_ACCOUNT_ID=
R2_ACCESS_KEY_ID=
R2_SECRET_ACCESS_KEY=
R2_BUCKET=

# Payments
STRIPE_SECRET_KEY=
STRIPE_WEBHOOK_SECRET=
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=
```

## CI/CD (.github/workflows/ci.yml)

```yaml
name: CI
on:
  push: { branches: [main] }
  pull_request:
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: pnpm/action-setup@v3
        with: { version: 9 }
      - uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: pnpm
      - run: pnpm install --frozen-lockfile
      - run: pnpm lint
      - run: pnpm typecheck
      - run: pnpm test
      - run: pnpm build
```

## Deploy

- Vercel: connect repo, set env vars, deploy.
- Cloudflare: use `@opennextjs/cloudflare` for Workers deploy.
- Self-host: `next start` behind nginx, or Dockerize.

## Before shipping

- Run [Checklists/pre-launch.md](../../Checklists/pre-launch.md).
- Run [ANTI-AI-DESIGN/checklist.md](../../ANTI-AI-DESIGN/checklist.md).

---

**Back to:** [Templates/](README.md)
