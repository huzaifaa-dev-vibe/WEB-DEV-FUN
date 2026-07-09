# TESTING (Overview)

> If you didn't test it, it doesn't work. Deep coverage in [Testing/](Testing/).

---

## Purpose

Verify your code does what you think it does. Catch regressions. Document intent. Enable refactoring.

## Prerequisites

- Basic JS/TS or your backend language.

## Learning Outcome

You can design a testing strategy, pick the right test types, write maintainable tests, and integrate them into CI.

## Related Files

- [Testing/](Testing/) — strategy
- [Jest/](Jest/), [Vitest/](Vitest/), [Cypress/](Cypress/), [Playwright/](Playwright/), [E2E/](E2E/)
- [TESTING.md](TESTING.md) (this file)
- [Checklists/testing.md](Checklists/testing.md)

## AI Instructions

When building any feature:
1. Write the test BEFORE or alongside the code.
2. Cover: happy path, validation errors, auth errors, not-found, edge cases.
3. Don't disable tests. If a test fails, fix the code or fix the test.
4. Run tests in CI. Block merge on regressions.
5. Don't chase coverage. Chase meaningful coverage.

## Human Notes

### Test Pyramid
```
       E2E (few)
      /         \
   Integration (some)
  /                \
Unit (many)
```

- **Unit** — fast, isolated, many.
- **Integration** — modules together, some.
- **E2E** — full system through the browser, few.

Inverted pyramid (mostly E2E) = slow, flaky, expensive.

### What to test
- **Behavior, not implementation.** If a refactor breaks your tests, your tests are too coupled to implementation.
- **Public APIs, not internals.**
- **Edge cases.** Empty, null, undefined, very large, very small, concurrent.
- **Error paths.** Not just happy path.

### What not to test
- Library internals (you don't own them).
- Getters/setters that just assign.
- Framework features (React rendering).
- Things that change constantly (snapshot entire components).

### Test qualities (GOOD)
- **Fast** — seconds, not minutes.
- **Isolated** — one failure doesn't cascade.
- **Repeatable** — same input → same result.
- **Self-validating** — pass/fail, not "looks ok".
- **Timely** — written with or before the code.

### Anti-patterns
- **Snapshot testing everything.** Brittle, low signal.
- **Mocking everything.** You're testing mocks, not code.
- **Testing implementation details.** Breaks on refactor.
- **Tests that depend on order.** Should be parallel-safe.
- **`sleep()` / `setTimeout()` in tests.** Use proper async waits.
- **Tests that pass for the wrong reason.** Assert outcomes, not absence of errors.
- **Coverage chasing.** 100% coverage of garbage is garbage.

## Quick Picks

| Need | Tool |
|---|---|
| JS/TS unit + integration | Vitest (new) / Jest (existing) |
| React component tests | Testing Library + Vitest/Jest |
| E2E (browser) | Playwright (default) / Cypress (alternative) |
| Visual regression | Chromatic / Percy / Playwright snapshots (sparingly) |
| Load testing | k6 / Artillery |
| API contract | Pact |
| Mock HTTP | MSW |
| Random data | Faker.js / @ngneat/falso |
| Time mocking | `vi.useFakeTimers()` / `sinon` |
| Snapshot (use sparingly) | Vitest/Jest snapshot |

## Example: Vitest unit test

```typescript
// math.test.ts
import { describe, it, expect } from 'vitest';
import { add } from './math';

describe('add', () => {
  it('adds two positive numbers', () => {
    expect(add(1, 2)).toBe(3);
  });

  it('handles negative numbers', () => {
    expect(add(-1, -2)).toBe(-3);
  });

  it('returns 0 when both are 0', () => {
    expect(add(0, 0)).toBe(0);
  });
});
```

## Example: React component test

```tsx
// Login.test.tsx
import { render, screen } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import { describe, it, expect } from 'vitest';
import { Login } from './Login';

describe('Login', () => {
  it('submits email and password', async () => {
    const onSubmit = vi.fn();
    render(<Login onSubmit={onSubmit} />);

    await userEvent.type(screen.getByLabelText(/email/i), 'a@b.com');
    await userEvent.type(screen.getByLabelText(/password/i), 'password');
    await userEvent.click(screen.getByRole('button', { name: /sign in/i }));

    expect(onSubmit).toHaveBeenCalledWith({
      email: 'a@b.com',
      password: 'password',
    });
  });

  it('shows error for invalid email', async () => {
    render(<Login onSubmit={vi.fn()} />);
    await userEvent.type(screen.getByLabelText(/email/i), 'not-an-email');
    await userEvent.click(screen.getByRole('button', { name: /sign in/i }));
    expect(await screen.findByText(/invalid email/i)).toBeInTheDocument();
  });
});
```

## Example: Playwright E2E

```typescript
// e2e/login.spec.ts
import { test, expect } from '@playwright/test';

test('user can log in', async ({ page }) => {
  await page.goto('/login');
  await page.getByLabel(/email/i).fill('test@example.com');
  await page.getByLabel(/password/i).fill('password');
  await page.getByRole('button', { name: /sign in/i }).click();
  await expect(page).toHaveURL('/dashboard');
  await expect(page.getByText(/welcome/i)).toBeVisible();
});
```

## CI Integration

```yaml
# .github/workflows/test.yml
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: npm
      - run: npm ci
      - run: npm run lint
      - run: npm run typecheck
      - run: npm run test:unit -- --coverage
      - run: npm run test:e2e
      - uses: codecov/codecov-action@v4
```

## References

- Vitest: https://vitest.dev/
- Testing Library: https://testing-library.com/
- Playwright: https://playwright.dev/
- Kent C. Dodds "How to know what to test": https://kentcdodds.com/blog/how-to-know-what-to-test
- "Write tests. Not too many. Mostly integration." — Guillermo Rauch

## Further Reading

- *Test-Driven Development* — Kent Beck
- *Growing Object-Oriented Software, Guided by Tests* — Steve Freeman, Nat Pryce
- *The Art of Unit Testing* — Roy Osherove

## Exercises

1. Write tests for an existing untested module. Achieve 80% meaningful coverage.
2. Convert a flaky E2E test to a reliable one.
3. Set up Playwright with visual comparison testing.

## Projects

- Build a CI pipeline that runs unit, integration, and E2E tests in parallel.
- Set up a "test the tests" (mutation testing with Stryker) experiment.

---

**Next:** [Testing/](Testing/) · [Vitest/](Vitest/) · [Playwright/](Playwright/)
