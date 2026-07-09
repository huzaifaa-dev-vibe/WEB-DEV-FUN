# NOTES

> Cross-cutting notes, opinions, and gotchas that don't fit in a single folder. Skim once, return as needed.

---

## Internet Fundamentals

### What happens when you type a URL?

1. **Parse URL** — browser splits scheme, host, path, query.
2. **DNS lookup** — host → IP (cached at browser, OS, router, ISP).
3. **Open TCP socket** — 3-way handshake to IP:443.
4. **TLS handshake** — negotiate cipher, verify cert, exchange keys.
5. **HTTP request** — `GET /path HTTP/1.1` + headers.
6. **Server processes** — routes, middleware, handler, DB.
7. **HTTP response** — status + headers + body.
8. **Browser parses HTML** — incremental render.
9. **Subresource fetches** — CSS, JS, images (in parallel, with priorities).
10. **JS executes** — DOM ready, then load event.
11. **Paint** — pixels on screen.

Total time = TTFB + render. → [Performance/](Performance/)

### Why this matters

Every millisecond you shave off DNS/TCP/TLS/TTFB compounds. Use `dns-prefetch`, `preconnect`, HTTP/2 or HTTP/3, edge CDNs, and keepalives.

---

## The Web Platform

The browser is a remarkably capable platform. Before reaching for a library, check if the platform does it:

| Need | Native API |
|---|---|
| Intersection-based lazy load | `IntersectionObserver` |
| Resize handling | `ResizeObserver` |
| Mutation watching | `MutationObserver` |
| Smooth scroll | `scrollIntoView({ behavior: 'smooth' })` |
| Sticky positioning | `position: sticky` |
| Dark mode | `prefers-color-scheme` |
| Reduced motion | `prefers-reduced-motion` |
| Forms validation | Constraint validation API |
| Modal | `<dialog>` |
| Accordion | `<details>` |
| Progress | `<progress>`, `<meter>` |
| Custom select | `<select>` with custom parts (limited) — otherwise Combobox pattern |
| Drag and drop | HTML5 DnD API (or Pointer Events for custom) |
| Clipboard | `navigator.clipboard` |
| Geolocation | `navigator.geolocation` |
| Notifications | `Notification` API |
| Service worker / offline | Service Worker API |
| Web sockets | `WebSocket` |
| Server-sent events | `EventSource` |
| Web workers | `Worker`, `SharedWorker` |
| Animations | Web Animations API |
| Local DB | `IndexedDB` (or `localStorage` for tiny stuff) |
| File system | File System Access API |
| Share | `navigator.share` |
| Payments | Payment Request API |
| Credentials | Credential Management API, WebAuthn |

When the platform doesn't do it well, reach for a library. → [EXTERNAL_REPOSITORIES.md](EXTERNAL_REPOSITORIES.md)

---

## Estimation

### Why estimates fail

- We estimate the happy path.
- We forget integration, testing, deploy, bug-fixing.
- We're optimistic to please.
- Unknowns are unknown.
- Requirements change.

### Better estimates

- **Three-point**: optimistic, likely, pessimistic. Report the range, not a single number.
- **Decompose**: break into <1-day chunks. Sum + 30% buffer.
- **Historical**: "this looks like feature X, which took 5 days."
- **T-shirt size first** (S/M/L), then days, then hours.
- **Update as you learn**. Re-estimate weekly.

### Anti-patterns

- "It'll take 2 weeks" → team commits to a date based on that, with no buffer.
- "I'll do it this weekend" → it won't be this weekend.
- "Almost done" for 3 weeks.

### The brutal truth

Software takes 2–3x longer than your first guess, on average. Plan accordingly.

---

## Reading Code

You'll spend more time reading than writing. Get good at it.

### Order
1. Read the README.
2. Read the entry point (e.g., `index.ts`, `app/page.tsx`).
3. Follow one request through the stack end-to-end.
4. Read the data model.
5. Read the tests — they document intent.
6. Skim the rest as needed.

### Tips
- Don't read linearly.
- Use go-to-definition aggressively.
- Use find-all-references to map call sites.
- Draw a diagram as you go.
- Note questions; answer them by reading, not by asking.

---

## Code Review

### As reviewer
- Review the test, not just the code.
- Question naming, structure, abstractions.
- Verify the bug actually exists (repro).
- Don't nitpick style (the linter should).
- Suggest, don't dictate.
- Praise good work.
- Don't block on minor stuff. Comment with "nit:".
- Ask "why?" when something is unclear.

### As author
- Self-review before requesting.
- Write a clear PR description (problem, solution, why this approach, how to test).
- Keep PRs small.
- Respond to every comment (even with "agree, will fix in follow-up").
- Don't take feedback personally.

### Toxic patterns
- "This is wrong" with no explanation.
- Bikeshedding on naming when the structure is the issue.
- Asking for changes the linter could enforce.
- Requesting a feature in a bug-fix PR.

---

## Performance Budgets

Set them early. Enforce in CI.

| Resource | Mobile budget | Desktop budget |
|---|---|---|
| HTML | 50 KB | 100 KB |
| CSS | 50 KB | 100 KB |
| JS (gzip) | 150 KB | 300 KB |
| Fonts | 100 KB | 200 KB |
| Images | 500 KB | 1 MB |
| Total | < 1 MB | < 2 MB |
| LCP | < 2.5s | < 2s |
| INP | < 200ms | < 200ms |
| CLS | < 0.1 | < 0.1 |

→ [Performance/budgets.md](Performance/budgets.md)

---

## The "Boring Tech" Rule

For the 80% case, choose:
- The thing your team knows.
- The thing with 5+ years of production use.
- The thing with docs, community, and StackOverflow answers.

Save the novel tech for the 20% where it actually matters.

This is why Postgres + Node + React + Next.js is the boring default. It's not exciting, but it ships.

---

## When to Rewrite

Almost never. Rewrite signals:
- The current system can't be incrementally fixed.
- The cost of adding features exceeds the cost of starting over.
- The team has the appetite and the runway.

Even then:
- Strangler fig pattern: replace piece by piece.
- Keep the old system running until the new one is proven.
- Don't rewrite + redesign + change team all at once.

The classic mistake: "Let's rewrite in <new framework>!" 18 months later, neither version ships.

---

## On Complexity

Complexity has two sources:
1. **Essential** — inherent to the problem.
2. **Accidental** — introduced by the tools/approach.

You can't reduce essential complexity. You can avoid accidental complexity. Most "hard" software is hard because of accidental complexity.

When something feels hard, ask:
- Is this problem genuinely hard?
- Or did I pick tools/approaches that made it hard?

The latter is fixable. → [Architecture/](Architecture/), [ANTI-PATTERNS.md](ANTI-PATTERNS.md)

---

## On Technical Debt

Not all debt is bad. Borrowing ships features. But:

- **Track it.** TODO comments, issues, a "debt" board.
- **Pay it down regularly.** 20% of sprint capacity, minimum.
- **Don't refactor "because it's ugly".** Refactor when changing the code is harder than it should be.
- **Don't refactor without tests.** You'll break things.

### Heuristic

If a junior engineer asks "why is it like this?" and the answer is "we've always done it that way" — that's a smell. Either the design has a reason (document it) or it's debt (pay it).

---

## Async Communication

The most effective engineering teams default to async.

- Write decisions down.
- Don't interrupt deep work.
- Meetings are for decisions that need real-time back-and-forth, not status.
- Use PRs / docs / issues as the primary medium.
- Sync meetings produce notes / decisions, not action.

### RFC workflow
1. Author writes RFC (problem, options, recommendation).
2. Comments for N days.
3. Decision meeting (or async decision).
4. Decision recorded in ADR. → [Architecture/adrs.md](Architecture/adrs.md)

---

## Hiring / Being Hired

### For hiring
- Don't do leetcode hazing for senior roles.
- Do pair on a real problem.
- Look for: clarity, curiosity, ownership, kindness.
- Test for the actual job, not trivia.

### For being hired
- Have a portfolio. Ship things.
- Read the job description. Tailor your story.
- Ask questions about the team, the codebase, the oncall.
- Be honest about what you don't know.

---

## Personal Productivity

- Single-task. Multitasking is a myth.
- Block deep work time. Defend it.
- Turn off notifications during deep work.
- End the day with a clear "next action" written down.
- Friday afternoon: review the week, plan the next.
- Keep a "today I learned" log.

---

## Career Advice

- Specialize early, generalize later. (Or vice versa, but know which you're doing.)
- Write in public. It compounds.
- Teach what you learn. You'll learn it better.
- Find mentors. Be a mentor.
- The salary jump is in the job change. The skill jump is in the side project.
- Don't optimize for the title. Optimize for the work.

---

## Tooling Hot Takes

- **Tailwind is the right default** for new projects. → [CSS/](CSS/)
- **shadcn/ui is the right component default.** → [EXTERNAL_REPOSITORIES.md](EXTERNAL_REPOSITORIES.md#component-libraries)
- **Postgres is the right default database** for 95% of new apps. → [PostgreSQL/](PostgreSQL/)
- **Prisma or Drizzle**; both fine; pick by team preference. → [ORM/](ORM/)
- **Next.js App Router** for the default React meta-framework. → [Templates/_next-app/](Templates/)
- **Vite** for SPAs that don't need SSR.
- **Vitest** over Jest for new projects.
- **Playwright** over Cypress for new projects.
- **Zod** for runtime validation.
- **Hono** for edge-first APIs.
- **Bun** is fast but Node 20 is still the safe default for production.
- **Vercel/Cloudflare** for frontend deploys. **AWS/GCP** for backend heavy lifting.
- **Linear** for issue tracking. (Opinionated, but most agree.)

These are defaults, not commandments. Deviate when you have a real reason.

---

## The 10x Engineer Myth

The actual 10x engineer:
- Writes less code (deletes more).
- Asks the right questions before writing.
- Catches the bug in design, not in QA.
- Makes teammates better.
- Documents as they go.
- Says "no" to scope creep.
- Doesn't work 80-hour weeks (they'd be slower, not faster).

The fake 10x engineer:
- Writes 10x the code (most of it bad).
- Doesn't review PRs.
- Hoards knowledge.
- Burns out teammates.

Be the first kind.

---

**Next:** [RESOURCES.md](RESOURCES.md) · [BOOKS.md](BOOKS.md) · [COMMUNITIES.md](COMMUNITIES.md)
