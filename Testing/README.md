# Testing

> If you didn't test it, it doesn't work.

---

## Purpose

Design a testing strategy. Pick the right test types. Write maintainable tests.

## Prerequisites

- [JavaScript/](../JavaScript/) or backend language.

## Learning Outcome

You can write tests that catch real bugs without slowing you down.

## Dependencies

- A test runner.

## Related Files

- [TESTING.md](../TESTING.md) · [Jest/](../Jest/) · [Vitest/](../Vitest/) · [Cypress/](../Cypress/) · [Playwright/](../Playwright/) · [E2E/](../E2E/) · [Testing/pyramid.md](pyramid.md)

## AI Instructions

When testing:
1. **Test behavior, not implementation.**
2. **One assertion per test** (mostly).
3. **Cover happy path + edge cases + errors.**
4. **No flaky tests** — fix or quarantine.
5. **Run in CI** on every PR.
6. **Don't chase coverage** — chase meaningful coverage.
7. **Don't disable tests.**
8. **Use realistic test data.**

## Human Notes

→ See [TESTING.md](../TESTING.md) for the full overview.

### Test pyramid
```
       E2E (few)
      /         \
   Integration (some)
  /                \
Unit (many)
```

→ [Testing/pyramid.md](pyramid.md)

### What to test
- Public APIs.
- Edge cases (empty, null, very large, very small, concurrent).
- Error paths.

### What NOT to test
- Library internals.
- Getters/setters.
- Framework features.
- Things that change constantly.

### Test qualities (FIRST)
- Fast.
- Isolated.
- Repeatable.
- Self-validating.
- Timely.

### Tools
- **Vitest** — default for new JS/TS.
- **Jest** — legacy default.
- **Playwright** — E2E (default).
- **Cypress** — E2E (alternative).
- **Testing Library** — component tests.
- **MSW** — mock HTTP.
- **Storybook** — component dev + visual tests.

## Common Mistakes

- ❌ Snapshot testing everything.
- ❌ Mocking everything.
- ❌ Testing implementation details.
- ❌ Order-dependent tests.
- ❌ `sleep()` in tests.
- ❌ Tests passing for wrong reasons.
- ❌ Coverage chasing.
- ❌ Ignoring flaky tests.

## Tools

→ [EXTERNAL_REPOSITORIES.md#testing](../EXTERNAL_REPOSITORIES.md#testing)

## References

- Testing Library: https://testing-library.com/
- Kent C. Dodds blog: https://kentcdodds.com/blog/

## Further Reading

- *Test-Driven Development* — Kent Beck
- *Growing Object-Oriented Software, Guided by Tests* — Freeman, Pryce

## Exercises

1. Add tests to an untested module. 80% meaningful coverage.
2. Fix a flaky test.
3. Set up Playwright for E2E.

## Projects

- Build a CI pipeline with unit + integration + E2E in parallel.

---

**Previous:** [Microservices/](../Microservices/) · **Next:** [Jest/](../Jest/) · **Related:** [CI-CD/](../CI-CD/)
