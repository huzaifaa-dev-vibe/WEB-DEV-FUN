# COMMON MISTAKES

> The mistakes every developer makes — and the fix. Skim before every code review.

This file is the inverse of [BEST_PRACTICES.md](BEST_PRACTICES.md): the patterns we keep seeing, why they're wrong, and what to do instead.

---

## HTML & Markup

### ❌ Using `<div>` for everything
**Why wrong:** Loses semantic meaning, breaks screen reader navigation, hurts SEO.
**Fix:** Use `<button>`, `<a>`, `<nav>`, `<main>`, `<article>`, `<section>`, `<header>`, `<footer>`, `<aside>`. Reach for `<div>` only when no semantic element fits.

### ❌ `<br>` for spacing
**Why wrong:** Couples content to presentation.
**Fix:** Use `margin`/`gap`. Use `<br>` only inside poetry/addresses.

### ❌ Forgetting `alt` on images
**Why wrong:** Accessibility failure, SEO loss.
**Fix:** Always `alt`. Decorative images: `alt=""`. Meaningful images: describe them.

### ❌ Input without `<label>`
**Why wrong:** Screen readers can't announce. Tap target unclear.
**Fix:** `<label for="id">` or wrap `<label><input/> Text</label>`.

### ❌ Skipping `<html>`, `<head>`, `<body>`
**Why wrong:** Browsers tolerate it, but it confuses parsers and is unprofessional.
**Fix:** Always include the full document skeleton.

---

## CSS

### ❌ `!important` everywhere
**Why wrong:** Specificity war. Unmaintainable.
**Fix:** Increase specificity naturally. Use layers (`@layer`) for overrides.

### ❌ Magic numbers (`margin-top: 47px`)
**Why wrong:** No system. Drifts.
**Fix:** Use a spacing scale (4 / 8 / 12 / 16 / 24 / 32 / 48 / 64 / 96 / 128). → [CSS/spacing.md](CSS/spacing.md)

### ❌ Hard-coded colors (`#3b82f6`)
**Why wrong:** Inconsistent theming. Can't do dark mode.
**Fix:** CSS variables / design tokens. → [CSS/variables.md](CSS/variables.md)

### ❌ `position: absolute` for layout
**Why wrong:** Fragile. Breaks on different content.
**Fix:** Flexbox or Grid. → [Flexbox/](Flexbox/), [Grid/](Grid/)

### ❌ `@media (max-width: ...)` everywhere
**Why wrong:** Mobile-after-the-fact. Easy to miss breakpoints.
**Fix:** Mobile-first: `@media (min-width: ...)`. → [Responsive-Design/](Responsive-Design/)

### ❌ Animations on `width`/`height`/`top`/`left`
**Why wrong:** Causes layout, janky.
**Fix:** Animate `transform` and `opacity` only. → [Animations/](Animations/)

### ❌ `z-index: 999999`
**Why wrong:** Numbers climb forever.
**Fix:** Tokenized z-index scale (0, 10, 20, 30, 40, 50, modal, toast). → [CSS/z-index.md](CSS/z-index.md)

---

## JavaScript

### ❌ `==` instead of `===`
**Why wrong:** Coercion bugs (`0 == ""` is true).
**Fix:** Always `===`/`!==`. ESLint rule `eqeqeq`.

### ❌ `var`
**Why wrong:** Function-scoped, hoisted, creates bugs.
**Fix:** `const` by default, `let` when reassigning. Never `var`.

### ❌ Mutating function arguments
**Why wrong:** Surprise side effects.
**Fix:** Treat args as read-only. Spread/copy if you need to change.

### ❌ `setTimeout` for async flow control
**Why wrong:** Race conditions. Non-deterministic.
**Fix:** `await`, event listeners, proper async primitives.

### ❌ Try/catch swallowing errors
```js
try { foo() } catch (e) {} // ❌
```
**Why wrong:** Hides bugs. Production becomes un-debuggable.
**Fix:** Log, rethrow, or handle. Never silent.

### ❌ `console.log` in production
**Why wrong:** Noise. PII leak. Performance.
**Fix:** Real logger (pino, winston). Stripped in prod build.

### ❌ No input validation
**Why wrong:** Garbage in, garbage out. Security hole.
**Fix:** Zod/Valibot at every boundary. → [JavaScript/validation.md](JavaScript/validation.md)

### ❌ `any` everywhere in TS
**Why wrong:** TS becomes JS with extra steps.
**Fix:** `unknown` + narrowing. Or proper types.

---

## React / Frontend Frameworks

### ❌ Direct DOM manipulation (`document.getElementById`)
**Why wrong:** Bypasses framework. State desync.
**Fix:** Use refs / state.

### ❌ Effects for derived state
```js
useEffect(() => setFullName(first + last), [first, last]) // ❌
```
**Why wrong:** Extra render. Stale state bugs.
**Fix:** `const fullName = first + last` directly in render.

### ❌ `useEffect` for data fetching without cleanup
**Why wrong:** Memory leak. Race condition on fast nav.
**Fix:** Use a data library (React Query, SWR, RTK Query) or AbortController.

### ❌ Passing setState down 5 levels
**Why wrong:** Coupling. Hard to refactor.
**Fix:** Context, store (Zustand), or co-locate state.

### ❌ Lists without stable keys
**Why wrong:** Re-render bugs. Input loses focus.
**Fix:** Stable, unique key (id, not index).

### ❌ Inline object/array props
```jsx
<Component style={{color: 'red'}} /> // ❌ new object every render
```
**Why wrong:** Memo busting. Re-renders.
**Fix:** Hoist constant objects. `useMemo` for computed.

### ❌ Premature `useMemo`/`useCallback`
**Why wrong:** Complexity for no gain.
**Fix:** Memoize only when measurably needed.

---

## Backend

### ❌ Trusting client input
**Why wrong:** Security hole. Bugs.
**Fix:** Validate at the edge, every time.

### ❌ `200 OK` with `{ error: "..." }`
**Why wrong:** Browsers, proxies, monitoring assume 2xx = success.
**Fix:** Correct HTTP status. → [REST/status-codes.md](REST/status-codes.md)

### ❌ N+1 queries
**Why wrong:** Performance disaster at scale.
**Fix:** `include`/`select`/eager loading. → [ORM/n-plus-1.md](ORM/n-plus-1.md)

### ❌ No transactions for multi-step writes
**Why wrong:** Partial writes corrupt data.
**Fix:** Wrap in a transaction. Always.

### ❌ Storing passwords in plaintext (or MD5)
**Why wrong:** Catastrophic breach.
**Fix:** bcrypt or argon2. → [Security/passwords.md](Security/passwords.md)

### ❌ JWT in localStorage
**Why wrong:** XSS steals it.
**Fix:** HttpOnly cookies + CSRF token. Or short-TTL JWT + refresh token.

### ❌ CORS `*` for credentialed requests
**Why wrong:** Any site can act as the user.
**Fix:** Allowlist specific origins.

### ❌ SQL string concatenation
**Why wrong:** SQL injection.
**Fix:** Parameterized queries. Always. → [Security/sql-injection.md](Security/sql-injection.md)

### ❌ Synchronous I/O on the main event loop (Node)
**Why wrong:** Blocks everything.
**Fix:** Async/await, streams, worker threads.

### ❌ No rate limiting on auth endpoints
**Why wrong:** Credential stuffing.
**Fix:** Rate limit + exponential backoff + captcha. → [Security/rate-limiting.md](Security/rate-limiting.md)

---

## Database

### ❌ No indexes on foreign keys / search columns
**Why wrong:** Slow queries, table scans.
**Fix:** Index FKs and frequent WHERE/ORDER BY columns. → [PostgreSQL/indexes.md](PostgreSQL/indexes.md)

### ❌ `SELECT *`
**Why wrong:** Wastes I/O. Breaks when schema changes.
**Fix:** Explicit column list.

### ❌ No migrations / manual schema changes
**Why wrong:** Drift between environments.
**Fix:** Migration tool (Prisma Migrate, Atlas, Flyway). → [PostgreSQL/migrations.md](PostgreSQL/migrations.md)

### ❌ Money as float
**Why wrong:** Floating point errors.
**Fix:** Integer cents, or `DECIMAL`/`NUMERIC`.

### ❌ Timestamps without timezone
**Why wrong:** Bugs across regions.
**Fix:** `TIMESTAMPTZ` (Postgres) or store UTC.

### ❌ Using UUID v4 as the only key on a hot table
**Why wrong:** Random inserts = index fragmentation.
**Fix:** UUID v7 / ULID (time-ordered) or bigserial. → [PostgreSQL/uuids.md](PostgreSQL/uuids.md)

### ❌ No connection pool limits
**Why wrong:** DB connection exhaustion.
**Fix:** Pool with max connections, queue, timeout. → [PostgreSQL/pooling.md](PostgreSQL/pooling.md)

---

## Security

### ❌ Secrets in code or repos
**Why wrong:** Git history is forever.
**Fix:** Env vars / vault. `git-secrets` pre-commit. → [Security/secrets.md](Security/secrets.md)

### ❌ No HTTPS
**Why wrong:** MITM. There's no excuse.
**Fix:** TLS everywhere. HSTS. → [Security/https.md](Security/https.md)

### ❌ Weak CSP (or none)
**Why wrong:** XSS exploits succeed.
**Fix:** Strict CSP with nonces/hashes. → [Security/headers.md](Security/headers.md)

### ❌ Clicking unverified links in logs (SSRF)
**Why wrong:** Internal network probing.
**Fix:** Validate/allowlist outbound URLs. → [Security/ssrf.md](Security/ssrf.md)

### ❌ Logging PII / secrets
**Why wrong:** Compliance violations. Breach amplification.
**Fix:** Redact before logging. Structured log schemas.

### ❌ `eval` / `Function()` / `innerHTML` with user input
**Why wrong:** XSS.
**Fix:** `textContent`, sanitization (DOMPurify), CSP.

---

## Performance

### ❌ Ship 2MB of JS for a landing page
**Why wrong:** Slow. Bounced users.
**Fix:** Bundle analyzer. Budget. Code-split. → [Performance/budgets.md](Performance/budgets.md)

### ❌ Unoptimized images (JPEG at 2MB)
**Why wrong:** LCP disaster.
**Fix:** AVIF/WebP, `srcset`, `loading="lazy"`, proper sizing. → [Performance/images.md](Performance/images.md)

### ❌ Render-blocking JS in `<head>`
**Why wrong:** Slow first paint.
**Fix:** `defer`/`async`, or move to bottom, or use modules.

### ❌ No caching headers
**Why wrong:** Re-downloading everything.
**Fix:** `Cache-Control`, `ETag`, CDN. → [Performance/caching.md](Performance/caching.md)

### ❌ Fonts causing FOIT/FOUT
**Why wrong:** Invisible text, jarring swaps.
**Fix:** `font-display: swap`, `preload` critical fonts, subset.

### ❌ Third-party scripts loading sync
**Why wrong:** One slow ad blocks the page.
**Fix:** `async`/`defer`, partytown, self-host.

---

## Accessibility

### ❌ Color contrast < 4.5:1
**Why wrong:** Unreadable for many users.
**Fix:** Test with axe / Lighthouse. → [Accessibility/contrast.md](Accessibility/contrast.md)

### ❌ Click handlers on `<div>`
**Why wrong:** No keyboard, no screen reader.
**Fix:** `<button>` or `role="button"` + `tabindex=0` + key handlers.

### ❌ Modal without focus trap
**Why wrong:** Tab leaks to background. Screen reader lost.
**Fix:** Focus trap library (focus-trap-react). → [Accessibility/modals.md](Accessibility/modals.md)

### ❌ No `:focus-visible` styles
**Why wrong:** Keyboard users can't see where they are.
**Fix:** Always style focus. → [Accessibility/focus.md](Accessibility/focus.md)

### ❌ Autoplaying carousels
**Why wrong:** Vestibular disorders. Annoying.
**Fix:** Don't. Or pause on hover/focus, respect `prefers-reduced-motion`.

---

## Git & Process

### ❌ Committing `node_modules` / build artifacts
**Why wrong:** Repo bloat. Merge conflicts.
**Fix:** `.gitignore`. → [Git/gitignore.md](Git/gitignore.md)

### ❌ `git push --force` to shared branches
**Why wrong:** Overwrites teammates' work.
**Fix:** `--force-with-lease`. Never force to `main`.

### ❌ Giant PRs ("1000+ files")
**Why wrong:** No one can review. Bugs slip in.
**Fix:** Small PRs. Stack if needed.

### ❌ Squash-merging 30 commits with one vague message
**Why wrong:** Loses context.
**Fix:** Conventional Commits. Detailed body.

### ❌ Long-lived feature branches
**Why wrong:** Merge hell.
**Fix:** Trunk-based. Feature flags. → [Git/workflows.md](Git/workflows.md)

---

## Deployment

### ❌ Deploying on Friday at 5pm
**Why wrong:** Weekend incident.
**Fix:** Deploy Mon–Thu mornings. Or: have great rollback + on-call.

### ❌ No rollback plan
**Why wrong:** When (not if) it breaks, you scramble.
**Fix:** Practice rollback. Document it. → [Deployment/rollback.md](Deployment/rollback.md)

### ❌ Different config in dev / prod
**Why wrong:** "Works on my machine" syndrome.
**Fix:** Same image, different env vars. Docker. → [Docker/](Docker/)

### ❌ No health check
**Why wrong:** Load balancer sends traffic to dead instance.
**Fix:** `/health` and `/ready`. → [Deployment/healthchecks.md](Deployment/healthchecks.md)

---

## AI Engineering

### ❌ Trusting LLM output without validation
**Why wrong:** Crashes, leaks, injections.
**Fix:** Schema-validate (Zod). Sanitize. → [AI/validation.md](AI/validation.md)

### ❌ No evals
**Why wrong:** You don't know if a prompt change regressed.
**Fix:** Eval set. Run on every change. → [AI/evals.md](AI/evals.md)

### ❌ Stuffing user input directly into the prompt
**Why wrong:** Prompt injection.
**Fix:** Treat user content as data, not instructions. → [Security/ai.md](Security/ai.md)

### ❌ No cost monitoring
**Why wrong:** One prompt loop = $10k bill.
**Fix:** Per-user cost tracking. Hard limits. Alerts. → [Performance/ai-cost.md](Performance/ai-cost.md)

### ❌ No streaming
**Why wrong:** 15s wait for first token = user leaves.
**Fix:** Stream tokens. Show typing indicator.

### ❌ Using GPT-4 when Mini suffices
**Why wrong:** 10x cost, slower.
**Fix:** Eval smaller models first. Route by task. → [LLM/routing.md](LLM/routing.md)

---

## Design / UI

### ❌ Centered hero + 2 CTAs + 3 feature cards
**Why wrong:** Looks AI-generated.
**Fix:** See [ANTI-AI-DESIGN/](ANTI-AI-DESIGN/). Pick a real layout.

### ❌ Emoji as icons
**Why wrong:** Cheap-looking. Inconsistent.
**Fix:** Real SVG icons. → [Icons/](Icons/)

### ❌ Purple-to-pink gradient
**Why wrong:** The AI tell.
**Fix:** Pick a palette with intent. → [Color-Palettes/](Color-Palettes/)

### ❌ `rounded-2xl` on everything
**Why wrong:** Looks soft and samey.
**Fix:** Mix radii intentionally. → [ANTI-AI-DESIGN/radii.md](ANTI-AI-DESIGN/radii.md)

### ❌ Lorem ipsum
**Why wrong:** Looks unfinished. Can't evaluate real layout.
**Fix:** Real copy. Always. → [ANTI-AI-DESIGN/copywriting.md](ANTI-AI-DESIGN/copywriting.md)

---

## Process / Culture

### ❌ "It works on my machine"
**Why wrong:** Deflects the problem.
**Fix:** Reproduce in CI. Containerize.

### ❌ Skipping code review because "it's urgent"
**Why wrong:** Bugs in prod are more urgent.
**Fix:** Faster review > no review.

### ❌ Hotfix directly in prod
**Why wrong:** No audit trail. No test.
**Fix:** Always via CI/CD, even if fast.

### ❌ No post-mortem after incidents
**Why wrong:** Same incident repeats.
**Fix:** Blameless post-mortem. → [Checklists/post-mortem.md](Checklists/post-mortem.md)

### ❌ "We'll add tests later"
**Why wrong:** You won't.
**Fix:** Tests in the same PR as the code.

---

**Next:** [ANTI-PATTERNS.md](ANTI-PATTERNS.md) · [ERRORS.md](ERRORS.md) · [DEBUGGING.md](DEBUGGING.md)
