# Cypress

> E2E and component testing. Runs in real browser.

---

## Purpose

Use Cypress for E2E and component tests.

## Prerequisites

- [Testing/](../Testing/), [JavaScript/](../JavaScript/).

## Learning Outcome

You can write Cypress E2E and component tests.

## Dependencies

- Node.js.

## Related Files

- [Playwright/](../Playwright/) · [E2E/](../E2E/) · [Testing/](../Testing/)

## AI Instructions

When using Cypress:
1. Use Cypress 13+.
2. Use `data-cy` attributes for selectors.
3. Don't `cy.wait(time)` — use `cy.intercept` + aliases.
4. Run in CI with `--headless --browser chrome`.
5. **For new projects, consider Playwright.**

## Human Notes

### E2E test
```js
describe('Login', () => {
  beforeEach(() => {
    cy.visit('/login');
  });

  it('logs in successfully', () => {
    cy.get('[data-cy=email]').type('test@example.com');
    cy.get('[data-cy=password]').type('password');
    cy.get('[data-cy=submit]').click();
    cy.url().should('include', '/dashboard');
    cy.contains('Welcome');
  });
});
```

### Intercept (mock API)
```js
cy.intercept('POST', '/api/login', { statusCode: 200, body: { token: '...' } }).as('login');
cy.get('[data-cy=submit]').click();
cy.wait('@login');
```

### Component testing
```tsx
import { mount } from '@cypress/react';
import { Login } from './Login';

it('renders form', () => {
  mount(<Login />);
  cy.get('[data-cy=email]').should('exist');
});
```

### Config
```js
// cypress.config.ts
import { defineConfig } from 'cypress';

export default defineConfig({
  e2e: {
    baseUrl: 'http://localhost:3000',
    specPattern: 'cypress/e2e/**/*.spec.ts',
  },
  component: {
    specPattern: 'src/**/*.cy.{ts,tsx}',
  },
});
```

### CI
```bash
npx cypress run --headless --browser chrome
```

### Why Cypress
- Real browser.
- Time travel (debug).
- Great DX.
- Component testing.

### Why NOT Cypress
- Chromium only (historically; Firefox/WebKit support is improving).
- No multi-tab.
- No iframe testing easily.
- Slower than Playwright.

## Common Mistakes

- ❌ `cy.wait(1000)` (use intercept aliases).
- ❌ Brittle selectors (`cy.get('.btn-blue')`).
- ❌ No `data-cy` attributes.
- ❌ Flaky tests ignored.

## Tools

- Cypress docs: https://docs.cypress.io/
- Cypress Testing Library: https://testing-library.com/docs/cypress-testing-library/intro/
- Percy / Chromatic (visual regression).

## References

- Cypress: https://www.cypress.io/

## Further Reading

- *End-to-End Testing with Cypress* — Daniel Irvine

## Exercises

1. Add Cypress E2E to a project.
2. Add component tests.
3. Run in CI.

## Projects

- Build E2E tests for an e-commerce flow.

---

**Previous:** [Vitest/](../Vitest/) · **Next:** [Playwright/](../Playwright/) · **Related:** [E2E/](../E2E/)
