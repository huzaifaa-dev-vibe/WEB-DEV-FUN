# Vitest

> Vite-native test runner. Fast. Jest-compatible. Default for new JS/TS.

---

## Purpose

Use Vitest for testing JS/TS apps.

## Prerequisites

- [Testing/](../Testing/), [JavaScript/](../JavaScript/).

## Learning Outcome

You can write, run, and configure Vitest tests.

## Dependencies

- Node.js, Vite (usually).

## Related Files

- [Jest/](../Jest/) · [Testing/](../Testing/) · [TESTING.md](../TESTING.md)

## AI Instructions

When using Vitest:
1. Use Vitest 1+.
2. Jest-compatible API (easy migration).
3. ESM native.
4. Uses Vite config — no separate config.
5. Use `@testing-library/react` for React.
6. Use `vi.mock` for mocks.
7. Run with `--coverage` for coverage (c8 or istanbul).

## Human Notes

### Config
```ts
// vitest.config.ts
import { defineConfig } from 'vitest/config';

export default defineConfig({
  test: {
    environment: 'node', // or 'jsdom', 'happy-dom'
    setupFiles: ['./vitest.setup.ts'],
    coverage: {
      provider: 'v8',
      reporter: ['text', 'html'],
    },
  },
  resolve: {
    alias: { '@': '/src' },
  },
});
```

### Test
```ts
import { describe, it, expect, vi } from 'vitest';
import { add } from './math';

describe('add', () => {
  it('adds numbers', () => {
    expect(add(1, 2)).toBe(3);
  });
});
```

### Async
```ts
it('fetches user', async () => {
  const user = await fetchUser(1);
  expect(user.name).toBe('Alice');
});
```

### Mocks
```ts
vi.mock('./api');
import { getUser } from './api';

it('returns user', async () => {
  vi.mocked(getUser).mockResolvedValue({ id: 1, name: 'Alice' });
  const user = await fetchUser(1);
  expect(user.name).toBe('Alice');
});
```

### Timers
```ts
beforeEach(() => vi.useFakeTimers());
afterEach(() => vi.useRealTimers());

it('schedules', () => {
  vi.advanceTimersByTime(5000);
});
```

### React component
```tsx
import { render, screen } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import { describe, it, expect, vi } from 'vitest';
import { Login } from './Login';

describe('Login', () => {
  it('submits', async () => {
    const onSubmit = vi.fn();
    render(<Login onSubmit={onSubmit} />);
    await userEvent.type(screen.getByLabelText(/email/i), 'a@b.com');
    await userEvent.click(screen.getByRole('button', { name: /sign in/i }));
    expect(onSubmit).toHaveBeenCalled();
  });
});
```

### UI testing (browser mode)
```bash
vitest --ui
```

### Coverage
```bash
vitest run --coverage
```

### Watch
```bash
vitest
```

### Why Vitest over Jest
- Faster.
- ESM native.
- Vite config (one config).
- Better TS support.
- Active development.

## Common Mistakes

- ❌ Snapshot testing everything.
- ❌ Testing implementation details.
- ❌ Mocking too much.

## Tools

- Vitest docs: https://vitest.dev/
- Testing Library: https://testing-library.com/
- @vitest/coverage-v8: coverage.

## References

- Vitest: https://vitest.dev/

## Exercises

1. Migrate a Jest project to Vitest.
2. Write component tests.
3. Add coverage thresholds.

## Projects

- Build a tested library with Vitest.

---

**Previous:** [Jest/](../Jest/) · **Next:** [Cypress/](../Cypress/) · **Related:** [TESTING.md](../TESTING.md)
