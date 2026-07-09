# DEBUGGING

> A systematic process for finding and fixing bugs. Don't skip steps.

This file is the universal debugging method. It works on any bug, in any stack. Use it.

---

## The 7-Step Method

### 1. Reproduce reliably
You cannot fix what you cannot reproduce. Get to a state where you can trigger the bug on demand.

- Find the exact steps.
- Note the environment (browser, OS, Node version, env vars, feature flag state).
- If intermittent, find the trigger pattern (load? time? race? specific data?).

**Output:** A repro recipe that triggers the bug in <1 minute.

### 2. Read the error
Actually read it. Top to bottom. Then bottom to top (stack traces often point at the real cause from the bottom).

- What is the error type?
- What file/line?
- What was the code trying to do?
- What was the actual value vs. expected?

If the error message is vague, look in logs, console, network tab.

**Check [ERRORS.md](ERRORS.md) first** — the error may already be cataloged.

### 3. Form a hypothesis
Based on the error and your mental model, what do you think is happening?

Write it down:
> "I think X is happening because Y, which would explain Z."

One hypothesis. Specific. Falsifiable.

### 4. Test the hypothesis (smallest experiment)
What's the smallest possible experiment to confirm or refute?

- Add one `console.log` (or one breakpoint) at the right spot.
- Check one variable's value.
- Try one input.

**Don't** change code yet. **Don't** apply a fix yet. Just observe.

### 5. If hypothesis wrong, form a new one
Don't retry the same fix. Don't apply random changes ("maybe if I add `await`..."). Form a new hypothesis based on what you just learned.

After 2 failed hypotheses, **stop and gather more information** — more logs, a smaller repro, a fresh pair of eyes.

### 6. Apply the fix
Once you've confirmed the root cause:

- Make the smallest possible change.
- Don't refactor while fixing.
- Run the repro to confirm fixed.
- Run the test suite to confirm no regressions.

### 7. Add a regression test
A bug you fix without a test will come back. Add a test that fails before the fix and passes after.

Commit message:
```
fix(auth): reject login attempts with empty password

Root cause: validatePassword() returned true for empty string due to
missing length check after trim().

Fix: add explicit length check.
Test: added test case for empty/whitespace-only passwords.
```

---

## Common Debugging Techniques

### Binary search (git bisect)
When did this break? Use `git bisect`:

```bash
git bisect start
git bisect bad HEAD
git bisect good <last-known-good-sha>
# git checks out a middle commit; test it
git bisect good  # or bad
# repeat until git tells you the offending commit
git bisect reset
```

### Binary search (code)
Comment out half. Does bug still happen? Narrow down.

### Binary search (data)
If a bug happens with some inputs but not others, find the smallest input that triggers it. Then find the smallest change to that input that doesn't.

### Print debugging
Don't be ashamed. But:
- Be specific: `console.log('user', JSON.stringify(user, null, 2))` not `console.log(user)`.
- Add a prefix so you can find them later: `console.log('[DEBUG-AUTH]', ...)`.
- Remove them before commit.

### Debugger
Use `debugger;` statement, or set breakpoints in DevTools / VS Code. Step through. Inspect variables. **Way** more powerful than print debugging.

### Network tab
For API bugs: check the request URL, method, headers, body, and the response status, headers, body. Many bugs are visible here.

### Performance tab
For slow: record a trace. Find the long task. Find what's in it.

### Memory tab
For leaks: take heap snapshot, do action, take another, compare.

### Reduce, reduce, reduce
Strip everything that doesn't matter. The smaller the repro, the faster the fix.

- New file, just the bug.
- Hardcoded inputs.
- No external deps if possible.

### Rubber duck
Explain the bug, line by line, to a duck (or coworker or LLM). Often the act of explaining reveals the issue.

### Fresh eyes
Step away. Come back tomorrow. Or ask someone else. Fresh eyes spot obvious things.

### Check the docs
Maybe the API doesn't do what you think. Read the actual docs (not the AI's summary).

### Check the source
For OSS bugs, read the source of the library. It's just code.

### Check recent changes
`git log -p <file>` — what changed recently?

### Check env
Different env between dev/prod? Different feature flags? Different data?

---

## Debugging Specific Stacks

### Frontend bugs
- **DevTools Console** for errors/warnings.
- **DevTools Elements** for DOM/CSS issues.
- **DevTools Network** for API issues.
- **React DevTools** for component tree, props, state, hooks.
- **Vue DevTools** for Vue.
- **Redux DevTools** for Redux state.
- **Lighthouse** for perf/a11y.
- **axe DevTools** for accessibility.

### Backend bugs
- **Logs** with request IDs (correlate across services).
- **APM** (Sentry, Datadog, NewRelic) for traces.
- **DB query logs** for slow queries.
- **EXPLAIN ANALYZE** for query plans. → [PostgreSQL/explain.md](PostgreSQL/explain.md)
- **Strace** for system calls.
- **tcpdump/Wireshark** for network.

### Build bugs
- **Clear caches**: `rm -rf node_modules .next dist`.
- **Reinstall**: `npm install`.
- **Lockfile drift**: `npm ci` instead of `npm install`.
- **Verbose**: `npm install --verbose`, `tsc --verbose`.

### CI bugs
- **Run the same commands locally** with the same Node version.
- **Add `set -x`** to see what's running.
- **SSH into the runner** (GitHub Actions: `tmate` action).

### Docker bugs
- **`docker logs <container>`**.
- **`docker exec -it <container> sh`**.
- **`docker inspect <container>`**.
- **`docker events`** for what's happening.

### Database bugs
- **`\dt`** — list tables.
- **`\d <table>`** — describe table.
- **`SELECT * FROM pg_stat_activity`** — running queries.
- **`EXPLAIN ANALYZE <query>`** — query plan.

### AI / LLM bugs
- **Log the full prompt** (input + output).
- **Test the prompt in the playground**.
- **Try a different model** to isolate.
- **Add evals** to detect regressions. → [AI/evals.md](AI/evals.md)

---

## Anti-Debugging Patterns (Don't Do These)

### 🚫 Random tweaking
"I'll just add `await` here." "Maybe change `let` to `const`." Stop. Form a hypothesis.

### 🚫 Catching and swallowing
```js
try { foo() } catch (e) { /* ??? */ }
```
Now you can't see the error. Remove the catch, or log it.

### 🚫 Disabling tests
"If I comment out this test, build passes!" Find out why it fails.

### 🚫 Blaming the framework
The framework is probably right. Your code is probably wrong. Verify before claiming a framework bug.

### 🚫 "It works on my machine"
Then your machine differs from prod. Find out how.

### 🚫 Adding `any`/`as any` to make TS shut up
The type error is telling you something. Listen.

### 🚫 Long debug sessions without breaks
After 2 hours, you're worse than fresh. Walk away. Come back.

### 🚫 Fixing symptoms
"Users see a 500, so I'll catch the error and return 200." You didn't fix it. You hid it.

---

## When to Ask for Help

After:
- 30 minutes with no progress on a small bug.
- 2 hours with no progress on a complex bug.
- 2 failed hypotheses.

How to ask:
> "Bug: <one sentence>.
> Repro: <steps>.
> Expected: <X>. Actual: <Y>.
> Hypotheses tried: <list>.
> What I think might be wrong but can't verify: <guess>.
> Smallest repro: <link or file>."

This format gets useful answers fast.

---

## Post-Fix Checklist

- [ ] Repro confirmed fixed.
- [ ] No regressions in test suite.
- [ ] Regression test added.
- [ ] Root cause documented in commit message.
- [ ] If systemic, added to [COMMON_MISTAKES.md](COMMON_MISTAKES.md) or [ANTI-PATTERNS.md](ANTI-PATTERNS.md).
- [ ] If user-facing, added to changelog.
- [ ] If incident, post-mortem scheduled. → [Checklists/post-mortem.md](Checklists/post-mortem.md)

---

**Next:** [ERRORS.md](ERRORS.md) · [COMMON_MISTAKES.md](COMMON_MISTAKES.md) · [AI_AGENT_GUIDE.md](AI_AGENT_GUIDE.md)
