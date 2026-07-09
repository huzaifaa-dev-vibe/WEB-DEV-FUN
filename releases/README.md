# Releases — WEB-DEV-FUN v1.0.0

> Pre-packaged configurations for popular AI coding agents. Drop into your project and the agent instantly knows how to use the WEB-DEV-FUN knowledge base.

## What's in v1.0.0

| Release | File | Target Agent | How to use |
|---|---|---|---|
| **Claude Skill** | [claude-skill/SKILL.md](claude-skill/SKILL.md) | Claude (Sonnet 4, Opus 4, Haiku 3.5) | Import as a Claude Skill via the Skills UI, or paste into a Claude project as system context. |
| **Codex (OpenAI)** | [codex/AGENTS.md](codex/AGENTS.md) | OpenAI Codex CLI / Codex in IDE | Place at project root as `AGENTS.md`. Codex auto-detects. |
| **Manus AI** | [manus-ai/TASK_PROMPT.md](manus-ai/TASK_PROMPT.md) | Manus AI | Paste the Task Prompt section into the Manus task input. Attach the repo as knowledge source. |

## Universal instructions (all three releases)

Every release encodes the same operating loop:

1. **Parse intent** — restate the user's request before acting.
2. **Route** — use the routing table to find the right folder.
3. **Plan** — write PLAN.md for projects > 1 file.
4. **Verify deps** — `npm view` / `gh repo view` before importing.
5. **Build** — apply `/BEST_PRACTICES.md`.
6. **Self-verify** — run `/AI_AGENT_GUIDE.md#how-to-verify-your-output`.
7. **Report** — what, how to run, next, risks.

## Universal rules (all three releases)

- TypeScript strict. No `any` without comment.
- Tailwind + shadcn/ui + Lucide icons. No emoji.
- Zod at every boundary. No silent catch.
- Vitest + Testing Library + Playwright.
- `/ANTI-AI-DESIGN/` is mandatory reading before any UI work.
- Conventional Commits.
- Verify before reporting done.

## Boring-but-correct default stack (all three releases)

| Layer | Pick |
|---|---|
| Frontend | Next.js 15 + TypeScript + Tailwind + shadcn/ui |
| Backend | Next.js API / Hono |
| DB | Postgres (Neon / Supabase) + Drizzle |
| Auth | Clerk or Better-Auth |
| Cache | Upstash Redis |
| Files | Cloudflare R2 |
| Email | Resend |
| Payments | Stripe |
| Analytics | PostHog |
| Errors | Sentry |
| Deploy | Vercel + Fly.io / Cloudflare |
| CI/CD | GitHub Actions |

---

## Compatibility

| Release | Compatible agents |
|---|---|
| Claude Skill | Claude Sonnet 4+, Claude Opus 4+, Claude Haiku 3.5+ (via Claude Skills or Projects) |
| Codex | OpenAI Codex CLI, Codex in VS Code, Codex in GitHub |
| Manus AI | Manus.ai web / API |

Other agents (Cursor, Cline, Aider, Continue, OpenHands) can use the [root `AI_AGENT_GUIDE.md`](../AI_AGENT_GUIDE.md) directly — paste it into `.cursorrules`, `.clinerules`, or your agent's config.

---

**Version:** 1.0.0
**Release date:** 2025-07-09
**License:** MIT
**Repository:** https://github.com/<your-username>/WEB-DEV-FUN
