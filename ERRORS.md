# ERRORS

> Common errors catalog. Search by message pattern. Each entry: cause, fix, verification.

Format per entry:
- **Pattern:** what the error looks like
- **Cause:** why it happens
- **Fix:** what to do
- **Verify:** how to confirm it's fixed
- **See:** deeper folder

---

## JavaScript / TypeScript

### `TypeError: Cannot read properties of undefined (reading 'foo')`
- **Cause:** Accessing a property on `undefined`. Often missing null check, async race, or wrong API response shape.
- **Fix:** Optional chaining `obj?.foo`. Validate the shape with Zod. Check the upstream source.
- **Verify:** Add a test with `undefined` input.
- **See:** [JavaScript/errors.md](JavaScript/errors.md)

### `TypeError: x is not a function`
- **Cause:** Wrong import, wrong `this` binding, default vs named export confusion.
- **Fix:** Check `export`/`import` style. Use `.bind(this)` or arrow functions.
- **Verify:** `console.log(typeof x)`.

### `SyntaxError: Unexpected token '<'`
- **Cause:** JS file is being served as HTML (404 page). Or import path is wrong.
- **Fix:** Check the script src / import path. Check server route.
- **Verify:** Open the URL in browser — should not be HTML.

### `Uncaught (in promise) SyntaxError: Unexpected token < in JSON`
- **Cause:** `res.json()` on a non-JSON response (often an HTML error page).
- **Fix:** Check `res.ok` and `Content-Type` before `.json()`.
- **Verify:** Log `res.status` and `res.headers.get('content-type')`.

### `ReferenceError: process is not defined` (in browser)
- **Cause:** Node global leaking into browser bundle.
- **Fix:** Use `import.meta.env` (Vite) or `process.env.NODE_ENV` shim. Don't import server-only code in client.
- **Verify:** Search bundle for `process`.

### `Maximum call stack size exceeded`
- **Cause:** Infinite recursion. Often missing base case or circular reference.
- **Fix:** Add base case. Detect cycles.
- **Verify:** Test with deep inputs.

### `Promise <pending>` logged instead of value
- **Cause:** Forgot `await`.
- **Fix:** Add `await`. Or use `.then()`.
- **Verify:** Value should be the resolved value, not a Promise.

### `TypeError: Cannot destructure property 'x' of 'undefined'`
- **Cause:** Object destructuring on `undefined`/`null`.
- **Fix:** Default value: `const { x } = obj || {}`.

### `Error: Hydration failed because the initial UI does not match what was rendered on the server`
- **Cause:** Server-rendered HTML differs from client's first render. Often due to `Date.now()`, `Math.random()`, `localStorage`, or `window` access during SSR.
- **Fix:** Gate browser-only logic behind `useEffect`. Use `suppressHydrationWarning` for legit differences (theme).
- **Verify:** Run production build + serve. Test on fresh browser.
- **See:** [JavaScript/ssr.md](JavaScript/ssr.md)

### `TS2307: Cannot find module '...' or its corresponding type declarations`
- **Cause:** Wrong import path, missing `@types/`, missing `tsx`/`tsconfig` paths.
- **Fix:** Install `@types/<pkg>`. Check `tsconfig.json#paths`. Use `.js` extension in imports if `"moduleResolution": "NodeNext"`.
- **Verify:** `tsc --noEmit` exits 0.

### `TS2322: Type 'X' is not assignable to type 'Y'`
- **Cause:** Type mismatch. Often missing field, wrong enum, or `any` propagation.
- **Fix:** Read the types. Either fix the value or fix the type. Don't `as any` unless you understand the cost.
- **Verify:** `tsc --noEmit` exits 0.

---

## React / Next.js

### `React Hook useEffect has a missing dependency: 'x'`
- **Cause:** Effect uses `x` but `x` isn't in deps array.
- **Fix:** Add it. Or, if intentional, eslint-disable with a comment explaining why. Often the fix is to redesign.
- **Verify:** Lint passes.

### `Warning: Each child in a list should have a unique "key" prop`
- **Cause:** Missing or non-unique key in `.map()`.
- **Fix:** Stable unique key (id, not index).
- **Verify:** No console warning.

### `Invalid hook call. Hooks can only be called inside the body of a function component.`
- **Cause:** Multiple React copies, hook in a class component, hook in a callback, or conditional hook.
- **Fix:** Single React in `node_modules`. Move hooks to top level of component.
- **Verify:** `npm ls react` shows one version.

### `Error: React Server Components are not supported in this configuration`
- **Cause:** Trying to use RSC in Pages Router, or missing `app/` directory setup.
- **Fix:** Use App Router (`app/`). Or `'use client'` directive where needed.
- **Verify:** Build passes.

### `404` on Next.js dynamic route after deploy
- **Cause:** Trailing slash mismatch, or `output: 'export'` not configured for dynamic routes.
- **Fix:** Check `next.config.js`. Use `generateStaticParams` for SSG.
- **Verify:** Test in `next build && next start`.

---

## CSS

### `Margin collapse`
- **Cause:** Vertical margins of adjacent blocks collapse.
- **Fix:** Use `padding`, `gap` (Flexbox/Grid), or `display: flow-root`.
- **See:** [CSS/margin-collapse.md](CSS/margin-collapse.md)

### `Z-index not working`
- **Cause:** No `position` set (other than `static`), or stacking context issue.
- **Fix:** Set `position: relative/absolute/fixed/sticky`. Understand stacking contexts.
- **See:** [CSS/z-index.md](CSS/z-index.md)

### `Flex item not shrinking/growing as expected`
- **Cause:** Missing `min-width: 0` (flex items default to `min-content`).
- **Fix:** `min-width: 0` on the flex child.

### `100vh` causes horizontal scroll on mobile`
- **Cause:** Browser UI overlaps viewport.
- **Fix:** Use `100dvh` (dynamic viewport height).
- **See:** [Responsive-Design/units.md](Responsive-Design/units.md)

### `Position: sticky` not working
- **Cause:** Parent has `overflow: hidden`, or no height, or ancestor has `transform`.
- **Fix:** Remove `overflow: hidden` on ancestors. Ensure parent has height.

---

## Node.js

### `Error: listen EADDRINUSE: address already in use :::3000`
- **Cause:** Another process on the port.
- **Fix:** `lsof -i :3000` then `kill -9 <pid>`. Or use a different port.
- **Verify:** Port is free.

### `Error: connect ECONNREFUSED 127.0.0.1:5432`
- **Cause:** DB not running, or wrong host/port.
- **Fix:** Start DB. Check env vars. Check firewall.
- **Verify:** `nc -zv localhost 5432`.

### `UnhandledPromiseRejectionWarning`
- **Cause:** Promise rejected with no `.catch()` or `try/catch`.
- **Fix:** Always handle rejections. Set up `process.on('unhandledRejection')`.

### `Cannot find module '...'`
- **Cause:** Not installed, wrong path, missing extension.
- **Fix:** `npm install`. Check path. Add `.js` extension if NodeNext.
- **Verify:** `node -e "require('...')"`.

### `Error: EMFILE: too many open files`
- **Cause:** Too many file descriptors (often from `fs` operations).
- **Fix:** Use `graceful-fs`. Increase `ulimit -n`. Stream instead of read-all.

### `EPIPE` / `write after end`
- **Cause:** Writing to a stream after it ended.
- **Fix:** Listen for `end`/`error`. Use proper stream pipelines.

---

## Database

### `relation "..." does not exist`
- **Cause:** Table not created, or in wrong schema, or case sensitivity (`"Users"` vs `users`).
- **Fix:** Run migrations. Check schema. Use lowercase identifiers.
- **Verify:** `\dt` in psql.

### `column "..." does not exist`
- **Cause:** Migration not run, typo, or case.
- **Fix:** Run migrations. Check column name.
- **Verify:** `\d tablename`.

### `duplicate key value violates unique constraint`
- **Cause:** Trying to insert a duplicate.
- **Fix:** Use `ON CONFLICT DO NOTHING` / `DO UPDATE`. Or check before insert.

### `deadlock detected`
- **Cause:** Two transactions waiting on each other.
- **Fix:** Always acquire locks in the same order. Keep transactions short.
- **See:** [PostgreSQL/deadlocks.md](PostgreSQL/deadlocks.md)

### `too many connections`
- **Cause:** Connection pool exhausted.
- **Fix:** Cap pool size. Use PgBouncer. Close idle connections.
- **See:** [PostgreSQL/pooling.md](PostgreSQL/pooling.md)

### `syntax error at or near "$1"`
- **Cause:** SQL parameter in a position that doesn't allow it (e.g., table name, ORDER BY direction).
- **Fix:** Use string interpolation for identifiers (with allowlist), parameters only for values.

---

## Build / Bundler

### `Module not found: Error: Can't resolve '...'`
- **Cause:** Not installed, wrong path, or it's a Node-only module imported in browser.
- **Fix:** Install. Check import path. Use polyfill or alternative.
- **Verify:** Build passes.

### `ReferenceError: window is not defined` (SSR)
- **Cause:** Browser-only code running on server.
- **Fix:** Gate behind `typeof window !== 'undefined'` or `useEffect`.

### `Cannot use import statement outside a module`
- **Cause:** Node trying to run ESM as CJS.
- **Fix:** Add `"type": "module"` to `package.json`, or use `.mjs`, or use `require`.

### `Top-level await is not available`
- **Cause:** Using `await` at module top level without ESM target.
- **Fix:** Use ESM target. Or wrap in async IIFE.

### `Build failed: ENOMEM`
- **Cause:** Out of memory during build.
- **Fix:** `NODE_OPTIONS=--max-old-space-size=4096 npm run build`. Or reduce bundle.

---

## Network / HTTP

### `CORS error: blocked by CORS policy`
- **Cause:** Server didn't send `Access-Control-Allow-Origin`.
- **Fix:** Configure CORS on server with allowlist. → [Security/cors.md](Security/cors.md)
- **Verify:** Check response headers in DevTools.

### `Mixed content blocked`
- **Cause:** HTTPS page loading HTTP resource.
- **Fix:** Use HTTPS for all resources. Or relative URLs.

### `NET::ERR_CERT_AUTHORITY_INVALID`
- **Cause:** Self-signed or expired cert.
- **Fix:** Use Let's Encrypt. Or accept in dev only.

### `502 Bad Gateway`
- **Cause:** Upstream service down or unreachable.
- **Fix:** Check service health. Check proxy config.

### `504 Gateway Timeout`
- **Cause:** Upstream too slow.
- **Fix:** Optimize. Increase timeout. Use async/queue.

### `Fetch failed: TypeError: fetch failed`
- **Cause:** Network error, DNS, TLS, or timeout.
- **Fix:** Check URL. Check DNS. Check proxy. Add timeout.

---

## Docker

### `Cannot connect to the Docker daemon`
- **Cause:** Docker not running, or no permissions.
- **Fix:** Start Docker. `sudo usermod -aG docker $USER`.

### `No space left on device`
- **Cause:** Docker filled disk.
- **Fix:** `docker system prune -a`. Increase disk.

### `Bind address already in use`
- **Cause:** Port conflict.
- **Fix:** Stop conflicting container. Or change port.

### `Image not found locally`
- **Cause:** Forgot to pull/build.
- **Fix:** `docker pull` / `docker build`.

---

## Git

### `fatal: refusing to merge unrelated histories`
- **Cause:** Two repos with no common ancestor.
- **Fix:** `git pull origin main --allow-unrelated-histories` (understand why first).

### `fatal: not a git repository`
- **Cause:** Not in a repo, or wrong dir.
- **Fix:** `cd` to repo root. `git init` if needed.

### `error: Your local changes would be overwritten by merge`
- **Cause:** Uncommitted changes conflict with pull.
- **Fix:** Commit, stash, or `git checkout -- .` (careful).

### `Permission denied (publickey)`
- **Cause:** SSH key not set up, or not added to GitHub.
- **Fix:** Generate key. Add to GitHub. `ssh-add`.

---

## CI/CD

### `Build passed locally but failed in CI`
- **Cause:** Different Node version, env vars, OS, missing files.
- **Fix:** Pin Node version (`nvm use` / `.nvmrc`). Match env. Use container.

### `Action not found`
- **Cause:** Wrong action name or version.
- **Fix:** Check the action's repo. Pin to a SHA or tagged version.

### `Secret not available`
- **Cause:** Not added to repo secrets, or wrong name.
- **Fix:** Add secret in repo settings. Match name exactly.

---

## AI / LLM

### `RateLimitError: 429`
- **Cause:** Hit API rate limit.
- **Fix:** Backoff. Cache. Reduce frequency. Upgrade tier.

### `ContextWindowExceededError`
- **Cause:** Too many tokens in prompt.
- **Fix:** Trim context. Use summarization. Use a longer-context model. → [LLM/context.md](LLM/context.md)

### `JSON parse error on LLM output`
- **Cause:** Model didn't return valid JSON.
- **Fix:** Use structured output / function calling. Add `response_format: { type: 'json_object' }`. Validate with Zod. Retry on failure. → [AI/validation.md](AI/validation.md)

### `Token usage way higher than expected`
- **Cause:** Long context, verbose prompts, not caching.
- **Fix:** Cache. Summarize history. Use smaller model. → [Performance/ai-cost.md](Performance/ai-cost.md)

---

## When You Can't Find Your Error

1. Check [DEBUGGING.md](DEBUGGING.md) for the systematic process.
2. Search the exact error message on:
   - StackOverflow
   - GitHub Issues (of the relevant package)
   - The package's docs
3. If still stuck, reduce to a minimal repro. → [DEBUGGING.md#minimal-repro](DEBUGGING.md)
4. Ask in the relevant community. → [COMMUNITIES.md](COMMUNITIES.md)

---

**Next:** [DEBUGGING.md](DEBUGGING.md) · [COMMON_MISTAKES.md](COMMON_MISTAKES.md) · [ANTI-PATTERNS.md](ANTI-PATTERNS.md)
