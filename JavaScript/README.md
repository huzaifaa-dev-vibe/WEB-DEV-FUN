# JavaScript

> The language of the web. From syntax to runtime to browser APIs to design patterns.

---

## Purpose

Master JavaScript as a language and as a runtime in the browser. Understand the event loop, closures, prototypes, async, and the modern ES2024+ feature set.

## Prerequisites

- [HTML/](../HTML/), [CSS/](../CSS/) basics.

## Learning Outcome

You can write idiomatic modern JS, debug async flows, use browser APIs, and ship production-grade client-side code.

## Dependencies

- HTML/CSS.

## Related Files

- [TypeScript/](../TypeScript/) · [NodeJS/](../NodeJS/) · [Bun/](../Bun/) · [Deno/](../Deno/) · [JavaScript/cheat-sheet.md](cheat-sheet.md) · [JavaScript/best-practices.md](best-practices.md) · [JavaScript/errors.md](errors.md) · [JavaScript/validation.md](validation.md)

## AI Instructions

When writing JS:
1. Use modern syntax: `const`/`let` (never `var`), arrow functions, destructuring, template literals, optional chaining, nullish coalescing.
2. Always `===`. ESLint `eqeqeq`.
3. Async/await over `.then()` chains.
4. Validate all external input (Zod). → [JavaScript/validation.md](validation.md)
5. Handle errors. Never silent `catch {}`.
6. No `console.log` in production code. Use a logger.
7. Don't mutate function arguments.
8. Use Web Platform APIs before libraries. → [NOTES.md#the-web-platform](../NOTES.md)
9. Don't reinvent what's in stdlib.
10. If using TS, no `any` without a comment.

## Human Notes

JavaScript is the most-deployed language in history. It's also the most-maligned. The truth: modern JS (ES2020+) is genuinely good. The hate is mostly deserved by old JS.

Key mental models:
- **Single-threaded + event loop.** One task at a time. I/O is async via callbacks/microtasks.
- **Prototypal inheritance.** Not class-based (despite `class` syntax sugar).
- **Closures.** Functions remember their lexical scope.
- **Everything is an object** (except primitives, which auto-box).
- **`this` is dynamic.** Arrow functions inherit it.

### The Event Loop

```
Call Stack ──┐
             │
Microtasks ──┤  (Promises, queueMicrotask)
             │
Macrotasks ──┘  (setTimeout, setInterval, I/O, events)
```

1. Run sync code on call stack.
2. When stack empty, drain microtask queue (all of them).
3. Run one macrotask.
4. Repeat.

This is why `Promise.resolve().then()` runs before `setTimeout(0)`.

## Modern Syntax Cheatsheet

```js
// Variables
const PI = 3.14;
let count = 0;

// Destructuring
const { name, age = 18 } = user;
const [first, ...rest] = arr;

// Spread / Rest
const merged = { ...a, ...b };
const [head, ...tail] = arr;
function sum(...nums) { return nums.reduce((a, b) => a + b, 0); }

// Optional chaining + nullish coalescing
const city = user?.address?.city ?? 'Unknown';

// Template literals
const greeting = `Hello, ${name}!`;

// Arrow functions
const add = (a, b) => a + b;

// async/await
async function fetchUser(id) {
  const res = await fetch(`/api/users/${id}`);
  if (!res.ok) throw new Error(`HTTP ${res.status}`);
  return res.json();
}

// Top-level await (ESM)
const config = await fetch('/config.json').then(r => r.json());

// Optional chaining with calls
const result = obj?.method?.();

// Nullish assignment
config.timeout ??= 5000;

// Logical assignment
config.enabled ||= true;
config.count &&= config.count + 1;

// Numeric separators
const billion = 1_000_000_000;

// BigInt
const huge = 9007199254740993n;

// Private class fields
class Counter {
  #count = 0;
  increment() { this.#count++; }
  get value() { return this.#count; }
}

// Object shorthand
const name = 'Alice';
const user = { name, age: 30 }; // { name: 'Alice', age: 30 }

// Computed property names
const key = 'dynamic';
const obj = { [key]: 'value' };

// Object spread
const updated = { ...user, age: 31 };
```

## Async Patterns

### Sequential
```js
for (const id of ids) {
  const user = await fetchUser(id);
  console.log(user);
}
```

### Parallel
```js
const users = await Promise.all(ids.map(fetchUser));
```

### With error tolerance
```js
const results = await Promise.allSettled(ids.map(fetchUser));
const fulfilled = results.filter(r => r.status === 'fulfilled').map(r => r.value);
const rejected = results.filter(r => r.status === 'rejected').map(r => r.reason);
```

### Race (first to settle, win or fail)
```js
const result = await Promise.race([
  fetchWithTimeout(url, 5000),
  timeout(5000),
]);
```

### Streams
```js
const res = await fetch('/stream');
const reader = res.body.getReader();
while (true) {
  const { done, value } = await reader.read();
  if (done) break;
  console.log(value); // Uint8Array
}
```

## Closures

```js
function counter() {
  let count = 0;
  return {
    increment: () => ++count,
    get: () => count,
  };
}

const c = counter();
c.increment();
c.increment();
c.get(); // 2
```

Closures power: data privacy, currying, partial application, memoization, React hooks.

## `this` Rules

1. Default: `undefined` (strict mode) or `globalThis`.
2. Implicit: `obj.method()` → `obj`.
3. Explicit: `fn.call(obj)`, `fn.apply(obj)`, `fn.bind(obj)`.
4. `new`: new empty object.
5. Arrow functions: inherit from lexical scope.

## Browser APIs

→ [NOTES.md#the-web-platform](../NOTES.md) for the full list.

Key ones:
- DOM manipulation (`document.querySelector`, etc.)
- Events (`addEventListener`, custom events)
- Fetch (HTTP)
- Web Storage (`localStorage`, `sessionStorage`, `IndexedDB`)
- WebSockets / SSE
- Web Workers / Service Workers
- IntersectionObserver / ResizeObserver / MutationObserver
- Web Animations API
- Clipboard, Geolocation, Notifications, Share
- WebRTC, MediaDevices
- File System Access API
- Gamepad, Battery, Vibration
- WebCrypto
- Performance API
- URL / URLSearchParams

## Modules

```js
// math.js
export const add = (a, b) => a + b;
export default function multiply(a, b) { return a * b; }

// main.js
import multiply, { add } from './math.js';
```

Native ESM in browsers: `<script type="module" src="app.js">`.

In Node: `"type": "module"` in package.json, or use `.mjs` extension.

## Errors

```js
try {
  await risky();
} catch (err) {
  if (err instanceof TypeError) { /* ... */ }
  else if (err instanceof NetworkError) { /* ... */ }
  else throw err; // re-throw unknown
}
```

Custom errors:
```js
class NetworkError extends Error {
  constructor(message, status) {
    super(message);
    this.name = 'NetworkError';
    this.status = status;
  }
}
```

## Iterators & Generators

```js
function* range(start, end, step = 1) {
  for (let i = start; i < end; i += step) yield i;
}

for (const n of range(0, 10)) console.log(n);
const [a, b, c] = range(0, 3); // 0, 1, 2
```

## Common Patterns

### Debounce
```js
const debounce = (fn, ms) => {
  let t;
  return (...args) => {
    clearTimeout(t);
    t = setTimeout(() => fn(...args), ms);
  };
};
```

### Throttle
```js
const throttle = (fn, ms) => {
  let last = 0;
  return (...args) => {
    const now = Date.now();
    if (now - last >= ms) { last = now; fn(...args); }
  };
};
```

### Once
```js
const once = (fn) => {
  let called = false;
  let result;
  return (...args) => {
    if (!called) { called = true; result = fn(...args); }
    return result;
  };
};
```

### Memoize
```js
const memoize = (fn) => {
  const cache = new Map();
  return (arg) => {
    if (cache.has(arg)) return cache.get(arg);
    const result = fn(arg);
    cache.set(arg, result);
    return result;
  };
};
```

### Pub/Sub
```js
const createEmitter = () => {
  const handlers = new Map();
  return {
    on(event, fn) {
      if (!handlers.has(event)) handlers.set(event, new Set());
      handlers.get(event).add(fn);
    },
    off(event, fn) { handlers.get(event)?.delete(fn); },
    emit(event, data) { handlers.get(event)?.forEach(fn => fn(data)); },
  };
};
```

## Common Mistakes

→ [COMMON_MISTAKES.md#javascript](../COMMON_MISTAKES.md)

Highlights:
- `==` instead of `===`.
- `var` instead of `let`/`const`.
- Mutating arguments.
- Silent catch.
- `console.log` in prod.
- No input validation.
- `any` everywhere in TS.

## References

- MDN JS: https://developer.mozilla.org/en-US/docs/Web/JavaScript
- TC39 proposals: https://github.com/tc39/proposals
- JavaScript.info: https://javascript.info/
- Exploring JS (Axel Rauschmayer): https://exploringjs.com/
- You Don't Know JS: https://github.com/getify/You-Dont-Know-JS
- ECMAScript spec: https://tc39.es/ecma262/

## Further Reading

- *Eloquent JavaScript* — Marijn Haverbeke (free)
- *You Don't Know JS* — Kyle Simpson (free)
- *Deep JavaScript* — Axel Rauschmayer (free)
- *Effective JavaScript* — David Herman

## Exercises

1. Implement debounce, throttle, once, memoize from scratch.
2. Build a pub/sub system + use it to sync two DOM elements.
3. Fetch data, render a list, handle loading/error/empty states.
4. Implement a fetch with retry + timeout + abort.
5. Build a virtual list (render only visible items).

## Projects

- Build a vanilla JS SPA with routing (no framework).
- Build a real-time chat with WebSockets.
- Build a markdown editor with live preview + localStorage autosave.

---

**Previous:** [CSS/](../CSS/) · **Next:** [TypeScript/](../TypeScript/) · **Related:** [NodeJS/](../NodeJS/), [Accessibility/](../Accessibility/)
