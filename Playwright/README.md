# Playwright

> Cross-browser E2E testing. From Microsoft. Default for new projects.

---

## Purpose

Use Playwright for E2E and component testing across browsers.

## Prerequisites

- [Testing/](../Testing/), [JavaScript/](../JavaScript/).

## Learning Outcome

You can write, run, and debug Playwright tests.

## Dependencies

- Node.js.

## Related Files

- [Cypress/](../Cypress/) · [E2E/](../E2E/) · [Testing/](../Testing/)

## AI Instructions

When using Playwright:
1. Use Playwright 1.40+.
2. Use `getByRole`, `getByLabel` for selectors (a11y-friendly).
3. Use `await page.goto()` etc.
4. Use `expect(locator).toBeVisible()` etc.
5. Run in CI with sharding for speed.
6. Use `playwright test --ui` for development.

## Human Notes

### Install
```bash
npm i -D @playwright/test
npx playwright install
```

### Config
```ts
// playwright.config.ts
import { defineConfig, devices } from '@playwright/test';

export default defineConfig({
  testDir: './e2e',
  fullyParallel: true,
  retries: process.env.CI ? 2 : 0,
  reporter: 'html',
  use: {
    baseURL: 'http://localhost:3000',
    trace: 'on-first-retry',
  },
  projects: [
    { name: 'chromium', use: { ...devices['Desktop Chrome'] } },
    { name: 'firefox', use: { ...devices['Desktop Firefox'] } },
    { name: 'webkit', use: { ...devices['Desktop Safari'] } },
    { name: 'mobile', use: { ...devices['iPhone 15'] } },
  ],
  webServer: {
    command: 'npm run dev',
    url: 'http://localhost:3000',
    reuseExistingServer: !process.env.CI,
  },
});
```

### Test
```ts
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

### Fixtures
```ts
import { test as base, expect } from '@playwright/test';

type Fixtures = { authedPage: Page };
export const test = base.extend<Fixtures>({
  authedPage: async ({ page }, use) => {
    // log in
    await use(page);
  },
});
```

### Auth state
```ts
// Save after login
await page.context().storageState({ path: 'auth.json' });

// Use in tests
const context = await browser.newContext({ storageState: 'auth.json' });
```

### API testing
```ts
import { test, expect } from '@playwright/test';

test('create user', async ({ request }) => {
  const res = await request.post('/api/users', { data: { name: 'Alice' } });
  expect(res.ok()).toBeTruthy();
});
```

### Visual testing
```ts
await expect(page).toHaveScreenshot('homepage.png');
```

### Run
```bash
npx playwright test
npx playwright test --ui
npx playwright test --headed
npx playwright test --project=chromium
npx playwright test --grep "login"
npx playwright show-report
```

### Why Playwright over Cypress
- All major browsers (Chrome, Firefox, Safari).
- Multi-tab, multi-origin.
- Faster.
- Better mobile emulation.
- Better parallelism.
- Auto-wait (less flake).
- Better CI integration.

### Why Cypress over Playwright
- Some teams prefer Cypress's API.
- Component testing is more mature in Cypress.

## Common Mistakes

- ❌ `page.waitForTimeout(1000)` (use `expect().toBe...` which auto-waits).
- ❌ Brittle selectors.
- ❌ No retries in CI.
- ❌ No trace on failure.

## Tools

- Playwright docs: https://playwright.dev/
- Playwright Test: https://playwright.dev/docs/intro
- Playwright Inspector (debug).
- HTML report.

## References

- Playwright: https://playwright.dev/

## Further Reading

- *Modern Web Testing with Playwright* — Unmesh Gundecha

## Exercises

1. Add Playwright E2E to a project.
2. Add auth state reuse.
3. Run in CI with sharding.

## Projects

- Build E2E tests for a SaaS app (signup, login, billing, dashboard).

---

**Previous:** [Cypress/](../Cypress/) · **Next:** [E2E/](../E2E/) · **Related:** [Testing/](../Testing/)
