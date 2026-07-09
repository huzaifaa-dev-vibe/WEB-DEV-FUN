# E2E

> End-to-end testing patterns. Reducing flake. Maximizing signal.

---

## Purpose

Master E2E: what to test, what NOT to test, how to reduce flake.

## Prerequisites

- [Testing/](../Testing/), [Playwright/](../Playwright/) or [Cypress/](../Cypress/).

## Learning Outcome

You can write reliable E2E tests for critical paths.

## Dependencies

- An E2E tool.

## Related Files

- [Playwright/](../Playwright/) · [Cypress/](../Cypress/) · [Testing/](../Testing/)

## AI Instructions

When writing E2E:
1. Test **critical paths only** (signup, login, purchase, key flow).
2. **Don't test everything** (use unit/integration for the rest).
3. **Use a11y selectors** (`getByRole`, `getByLabel`).
4. **Auto-wait** — don't `sleep`.
5. **Test data setup** — use API calls, not UI clicks.
6. **Parallelize** in CI.
7. **Quarantine flaky tests** — fix or remove.

## Human Notes

### What to E2E test
- Signup / login / logout.
- Password reset.
- Core business flow (purchase, post creation, etc.).
- Critical error states (out of stock, payment failed).

### What NOT to E2E test
- Every form field.
- Every UI state.
- Visual details (use visual regression).
- Performance (use Lighthouse CI).

### Reducing flake
- **Auto-wait** for elements (Playwright does this).
- **Don't use `sleep` / `setTimeout`**.
- **Retry failed assertions** (Playwright does).
- **Stable test data** (don't depend on prod data).
- **Isolate tests** (don't share state).
- **Reset DB between tests** (or use unique data per test).
- **Run multiple times locally** before pushing.

### Test data
- **Use API for setup** — faster than UI clicks.
- **Unique data per test** — avoid conflicts.
- **Clean up after tests** — or use ephemeral DB.

### Page Object Model
Encapsulate page interactions:
```ts
class LoginPage {
  constructor(private page: Page) {}
  async login(email: string, password: string) {
    await this.page.getByLabel(/email/i).fill(email);
    await this.page.getByLabel(/password/i).fill(password);
    await this.page.getByRole('button', { name: /sign in/i }).click();
  }
}
```

Or use **fixtures** (Playwright-style).

### Parallelism
- Run tests in parallel.
- Shard across CI machines.
- Don't share state.

### CI
- Run on every PR.
- Block merge on critical failures.
- Run full suite nightly.
- Upload traces/reports as artifacts.

### Visual regression
- Screenshot comparisons.
- Use sparingly (catches unintended UI changes).
- Tools: Percy, Chromatic, Playwright `toHaveScreenshot`.

### Performance testing in E2E
- Lighthouse CI in Playwright.
- Web Vitals assertions.

## Common Mistakes

- ❌ Testing every UI interaction.
- ❌ Brittle selectors.
- ❌ `sleep` / `waitForTimeout`.
- ❌ Shared state between tests.
- ❌ No parallelism (suite takes 30 min).
- ❌ Ignoring flaky tests.
- ❌ Testing in prod data.

## Tools

- Playwright, Cypress.
- Percy, Chromatic (visual).
- Lighthouse CI.
- Currents / Sorry Cypress (Cypress dashboard alternatives).

## References

- Playwright best practices: https://playwright.dev/docs/best-practices
- Testing Library principles: https://testing-library.com/docs/guiding-principles

## Exercises

1. Reduce flake in a flaky E2E suite.
2. Parallelize your E2E suite.
3. Add visual regression to critical pages.

## Projects

- Build an E2E suite covering signup → purchase → refund.

---

**Previous:** [Playwright/](../Playwright/) · **Next:** [AI/](../AI/) · **Related:** [Testing/](../Testing/)
