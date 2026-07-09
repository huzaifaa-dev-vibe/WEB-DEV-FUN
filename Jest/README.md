# Jest

> Mature JS test runner. Legacy default. Use Vitest for new projects.

---

## Purpose

Use Jest for testing JS/TS apps.

## Prerequisites

- [Testing/](../Testing/), [JavaScript/](../JavaScript/).

## Learning Outcome

You can write, run, and configure Jest tests.

## Dependencies

- Node.js.

## Related Files

- [Vitest/](../Vitest/) · [Testing/](../Testing/) · [TESTING.md](../TESTING.md)

## AI Instructions

When using Jest:
1. Use Jest 29+.
2. Use `ts-jest` or `@swc/jest` for TS.
3. Use `@testing-library/react` for React.
4. Use `jest.mock` for mocks.
5. Don't snapshot test everything.
6. **For new projects, use Vitest.**

## Human Notes

### Config
```js
// jest.config.js
module.exports = {
  preset: 'ts-jest',
  testEnvironment: 'node', // or 'jsdom' for frontend
  setupFilesAfterEnv: ['<rootDir>/jest.setup.ts'],
  moduleNameMapper: { '^@/(.*)$': '<rootDir>/src/$1' },
  coverageDirectory: 'coverage',
  collectCoverageFrom: ['src/**/*.{ts,tsx}', '!src/**/*.d.ts'],
};
```

### Test
```js
describe('add', () => {
  it('adds numbers', () => {
    expect(add(1, 2)).toBe(3);
  });

  it('handles negative', () => {
    expect(add(-1, -2)).toBe(-3);
  });
});
```

### Async
```js
it('fetches user', async () => {
  const user = await fetchUser(1);
  expect(user.name).toBe('Alice');
});
```

### Mocks
```js
jest.mock('./api');
const api = require('./api');
api.getUser.mockResolvedValue({ id: 1, name: 'Alice' });

it('returns user', async () => {
  const user = await getUser(1);
  expect(user.name).toBe('Alice');
  expect(api.getUser).toHaveBeenCalledWith(1);
});
```

### React component
```tsx
import { render, screen } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import { Login } from './Login';

it('submits', async () => {
  const onSubmit = jest.fn();
  render(<Login onSubmit={onSubmit} />);
  await userEvent.type(screen.getByLabelText(/email/i), 'a@b.com');
  await userEvent.click(screen.getByRole('button', { name: /sign in/i }));
  expect(onSubmit).toHaveBeenCalled();
});
```

### Coverage
```bash
jest --coverage
```

### Watch
```bash
jest --watch
```

## Common Mistakes

- ❌ Snapshot testing everything.
- ❌ Testing implementation details.
- ❌ Mocking too much.
- ❌ Tests that depend on order.

## Tools

- Jest docs: https://jestjs.io/docs
- Testing Library: https://testing-library.com/

## References

- Jest: https://jestjs.io/

## Exercises

1. Add Jest to a project. Write 10 tests.
2. Mock an external API.
3. Add coverage thresholds.

## Projects

- Test a library you wrote.

---

**Previous:** [Testing/](../Testing/) · **Next:** [Vitest/](../Vitest/) · **Related:** [TESTING.md](../TESTING.md)
