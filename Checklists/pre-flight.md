# Pre-Flight Checklist

> Run before opening a PR. Catches 80% of issues before review.

---

## Code
- [ ] Lint passes (`npm run lint`).
- [ ] Type-check passes (`tsc --noEmit`).
- [ ] Tests pass (`npm test`).
- [ ] Build passes (`npm run build`).
- [ ] No `console.log` in committed code.
- [ ] No `any` in TS without a comment.
- [ ] No commented-out code.
- [ ] No TODO/FIXME without a linked issue.

## Tests
- [ ] New behavior has tests.
- [ ] Edge cases covered (empty, null, very large, concurrent).
- [ ] Error paths covered.
- [ ] Tests run in parallel (no order dependency).
- [ ] No flaky tests introduced.

## PR Hygiene
- [ ] PR < 400 lines diff (or justified).
- [ ] One concern per PR.
- [ ] Conventional commit message.
- [ ] PR description: problem + solution + how to test.
- [ ] Self-reviewed.

## Security
- [ ] No secrets in code.
- [ ] No PII in logs.
- [ ] All inputs validated (Zod).
- [ ] All SQL parameterized.
- [ ] No `dangerouslySetInnerHTML` without sanitization.
- [ ] No new deps without justification.

## Performance
- [ ] No new heavy deps.
- [ ] Bundle size not increased > 10KB.
- [ ] No N+1 queries introduced.
- [ ] Images optimized (if new).

## Accessibility
- [ ] All interactive elements keyboard-accessible.
- [ ] `:focus-visible` styled.
- [ ] All images have `alt`.
- [ ] All inputs have `<label>`.
- [ ] Contrast ≥ 4.5:1.

## Mobile
- [ ] Tested at 375px viewport.
- [ ] No horizontal scroll.
- [ ] Tap targets ≥ 44×44px.

## Docs
- [ ] README updated (if needed).
- [ ] JSDoc / TSDoc for new public APIs.
- [ ] CHANGELOG updated (user-facing changes).

---

**Next:** [pre-launch.md](pre-launch.md) · Back to [Checklists/](README.md)
