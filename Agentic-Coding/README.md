# Agentic Coding

> AI coding agents: Cursor, Cline, Aider, OpenHands. How to use them well.

---

## Purpose

Master AI coding tools for productivity without sacrificing quality.

## Prerequisites

- [AI_AGENT_GUIDE.md](../AI_AGENT_GUIDE.md), coding experience.

## Learning Outcome

You can use AI coding tools to ship faster without producing garbage.

## Dependencies

- An AI coding tool.

## Related Files

- [AI_AGENT_GUIDE.md](../AI_AGENT_GUIDE.md) · [PROMPTS.md](../PROMPTS.md) · [Prompt-Engineering/](../Prompt-Engineering/) · [Agentic-Coding/observability.md](observability.md) · [EXTERNAL_REPOSITORIES.md#agentic-coding-tools](../EXTERNAL_REPOSITORIES.md#agentic-coding-tools)

## AI Instructions

When using agentic tools:
1. **Specify intent** clearly.
2. **Provide context** (files, requirements, constraints).
3. **Verify every change** before committing.
4. **Use as pair programmer**, not autopilot.
5. **Run tests** after every change.
6. **Self-check** before claiming done. → [AI_AGENT_GUIDE.md](../AI_AGENT_GUIDE.md)

## Human Notes

### Tools
- **Cursor** — VS Code fork, AI-first. Best DX. Paid.
- **Claude Code** — Anthropic's CLI agent. Paid.
- **Cline** (formerly Claude Dev) — open-source VS Code extension. Bring your own API key.
- **Aider** — terminal-based. Open-source.
- **Continue** — open-source VS Code extension. Configurable.
- **OpenHands** (formerly OpenDevin) — open-source autonomous agent.
- **GitHub Copilot** — inline suggestions + agent mode.
- **Codeium** — free tier, competitive.
- **Windsurf** — Codeium's agentic IDE.
- **v0** — UI generation (Vercel).
- **Bolt.new** — full-stack generation.
- **Replit Agent** — in-browser.
- **Lovable** — full-stack generation.

### Patterns for success
1. **Plan first**: ask AI to outline before writing code.
2. **Small steps**: one feature/bug per session.
3. **Read diffs carefully**: AI introduces bugs.
4. **Run tests**: after every change.
5. **Iterate**: prompt, review, refine.
6. **Use as pair programmer**: ask "why?" not just "do X".
7. **Customize**: .cursorrules, .clinerules, etc.

### .cursorrules / .clinerules
Project-level instructions for the agent:
```markdown
# Project Rules

## Tech Stack
- Next.js 15 (App Router)
- TypeScript (strict)
- Tailwind CSS
- shadcn/ui
- Prisma + Postgres

## Code Style
- Functional components only.
- No `any`.
- Always validate input with Zod.
- Use TanStack Query for data fetching.

## Patterns
- Server Components by default; `'use client'` only when needed.
- Co-locate component + test.
- Use Lucide icons (no emoji).
- Use [ANTI-AI-DESIGN](/ANTI-AI-DESIGN/) principles.

## Forbidden
- `console.log` in committed code.
- `dangerouslySetInnerHTML` without DOMPurify.
- Inline styles.
- `as any`.
```

### Workflow
1. **Open task**: describe in plain English.
2. **AI proposes plan**.
3. **You approve / refine**.
4. **AI executes**.
5. **You review diff**.
6. **AI runs tests**.
7. **You verify**.
8. **Commit**.

### When AI excels
- Boilerplate (CRUD, forms).
- Refactoring (rename, extract).
- Writing tests.
- Documentation.
- "I know what I want but not how to write it".
- Migrating code (e.g., JS → TS).

### When AI struggles
- Architectural decisions.
- Performance optimization (needs profiling).
- Security (needs verification).
- Novel / rare APIs.
- Cross-repo refactors.
- Subtle bugs.

### Verification (always)
- Tests pass.
- Types pass.
- Lint passes.
- Build succeeds.
- Visual check (for UI).
- Manual smoke test.

→ [AI_AGENT_GUIDE.md#how-to-verify-your-output](../AI_AGENT_GUIDE.md)

### Cost management
- Cursor / Claude Code: subscriptions.
- API-based (Cline, Continue): pay per token.
- Set spending limits.
- Cache common queries.

### Observability
- Log AI suggestions / acceptances.
- Track productivity (PRs/week, time/PR).
- Track regressions.

→ [Agentic-Coding/observability.md](observability.md)

### Pitfalls
- **AI-looking code**. → [ANTI-AI-DESIGN/](../ANTI-AI-DESIGN/)
- **Hallucinated APIs**. Verify.
- **Over-confident AI**. Verify.
- **Tech debt accumulation**. Review carefully.
- **Skill atrophy**. Don't blindly accept.

## Common Mistakes

- ❌ Blindly accepting AI suggestions.
- ❌ No verification.
- ❌ No project rules file.
- ❌ Asking AI for things it can't do (architecture).
- ❌ Not iterating.
- ❌ Not reading the diff.

## Tools

→ [EXTERNAL_REPOSITORIES.md#agentic-coding-tools](../EXTERNAL_REPOSITORIES.md#agentic-coding-tools)

## References

- Cursor docs: https://docs.cursor.sh/
- Cline: https://github.com/cline/cline
- Aider: https://aider.chat/
- Continue: https://www.continue.dev/

## Further Reading

- Andrej Karpathy on agentic coding.
- "How to use Cursor effectively" blog posts.

## Exercises

1. Set up `.cursorrules` for your project.
2. Build a feature end-to-end with Cursor.
3. Review every line of an AI-generated PR.

## Projects

- Build a SaaS app using Cursor + this repo as reference.

---

**Previous:** [MCP/](../MCP/) · **Next:** [Prompt-Engineering/](../Prompt-Engineering/) · **Related:** [AI_AGENT_GUIDE.md](../AI_AGENT_GUIDE.md)
