# Design Patterns

> Codified solutions to common problems. Use them. Don't cargo-cult them.

---

## Purpose

Catalog the most useful design patterns for web development — GoF, JS-specific, and reactive.

## Prerequisites

- Solid [JavaScript/](../JavaScript/) or [TypeScript/](../TypeScript/).

## Learning Outcome

You can recognize when a pattern applies, apply it, and know when NOT to apply it.

## Dependencies

- JS/TS.

## Related Files

- [Clean-Code/](../Clean-Code/) · [Architecture/](../Architecture/) · [ANTI-PATTERNS.md](../ANTI-PATTERNS.md) · [Design-Patterns/gof.md](gof.md) · [Design-Patterns/reactive.md](reactive.md)

## AI Instructions

When solving a recurring problem:
1. Check if a known pattern fits.
2. Apply the smallest version of the pattern that solves the problem.
3. Don't introduce patterns speculatively. YAGNI.

## Human Notes

Patterns are tools, not goals. Applying Singleton to everything is as bad as not knowing it exists.

## Creational

### Singleton
```ts
class Database {
  private static instance: Database;
  private constructor() {}
  static getInstance() { return this.instance ??= new Database(); }
}
```
Use: global state, DB connection.
Don't use: testing (mocking hell), modular code.

### Factory
```ts
function createUser(type: 'admin' | 'user', data: UserProps): User {
  if (type === 'admin') return new AdminUser(data);
  return new RegularUser(data);
}
```
Use: when object creation has logic.

### Builder
```ts
const query = new QueryBuilder()
  .select('*')
  .from('users')
  .where('active', true)
  .orderBy('name')
  .build();
```
Use: complex object construction (queries, configs).

### Prototype
```ts
const obj = { greet() { return 'hi'; } };
const clone = Object.create(obj);
```
Use: object cloning.

## Structural

### Adapter
```ts
// Old API returns { full_name: 'Alice' }
// New code expects { name: 'Alice' }
class UserAdapter {
  constructor(private legacy: LegacyUser) {}
  get name() { return this.legacy.full_name; }
}
```

### Facade
```ts
// Wrap a complex subsystem with a simpler API
class CheckoutFacade {
  constructor(
    private cart: Cart,
    private payments: Payments,
    private inventory: Inventory,
  ) {}
  async checkout() { /* orchestrate */ }
}
```

### Decorator
```ts
function log<T extends (...args: any[]) => any>(fn: T): T {
  return ((...args: any[]) => {
    console.log('calling', fn.name);
    return fn(...args);
  }) as T;
}
```

### Proxy
```ts
const handler: ProxyHandler<User> = {
  get(target, prop) {
    console.log('get', prop);
    return target[prop as keyof User];
  },
  set(target, prop, value) {
    console.log('set', prop, value);
    target[prop as keyof User] = value;
    return true;
  },
};
const user = new Proxy(rawUser, handler);
```

### Composite
Tree structures (UI components, file systems).

### Flyweight
Share state to reduce memory (rare in web).

## Behavioral

### Observer / Pub-Sub
```ts
const emitter = createEmitter(); // see JavaScript/README.md
emitter.on('user:created', handler);
emitter.emit('user:created', user);
```

### Strategy
```ts
class Sorter {
  constructor(private strategy: (a, b) => number) {}
  sort(arr) { return arr.sort(this.strategy); }
}
new Sorter((a, b) => a - b).sort([3, 1, 2]);
```

### Command
```ts
class AddItemCommand {
  constructor(private cart: Cart, private item: Item) {}
  execute() { this.cart.add(this.item); }
  undo() { this.cart.remove(this.item); }
}
```
Use: undo/redo, queues.

### Iterator
```ts
class Range {
  *[Symbol.iterator]() { for (let i = 0; i < 10; i++) yield i; }
}
for (const n of new Range()) console.log(n);
```

### State
```ts
class TrafficLight {
  private state: LightState = new GreenState(this);
  transition() { this.state = this.state.next(); }
  get color() { return this.state.color; }
}
```

### Template Method
```ts
abstract class DataFetcher {
  async fetch() {
    const url = this.getUrl();
    const data = await this.request(url);
    return this.transform(data);
  }
  protected abstract getUrl(): string;
  protected request(url: string) { return fetch(url).then(r => r.json()); }
  protected transform(data: any) { return data; }
}
```

### Chain of Responsibility
Middleware pattern in Express.

### Visitor
Rare in web.

## Reactive Patterns

### Observable
```ts
// RxJS or native
import { from } from 'rxjs';
from([1, 2, 3]).subscribe(x => console.log(x));
```

### Subject
Multicast observable.

### BehaviorSubject
State-holding observable.

### Reactive Streams (with Signals)
Solid.js / Vue ref / Svelte stores / React (with `use`).

## JavaScript-Specific Patterns

### Module pattern
```ts
// ESM
export const add = (a, b) => a + b;
import { add } from './math.js';
```

### Mixin
```ts
type Constructor<T = {}> = new (...args: any[]) => T;
function Timestamped<TBase extends Constructor>(Base: TBase) {
  return class extends Base {
    timestamp = Date.now();
  };
}
```

### Curry
```ts
const add = (a: number) => (b: number) => a + b;
const add5 = add(5);
add5(3); // 8
```

### Partial application
```ts
const log = (level: string, msg: string) => console.log(`[${level}] ${msg}`);
const error = log.bind(null, 'ERROR');
error('something broke');
```

### Memoize
See [JavaScript/README.md#common-patterns](../JavaScript/README.md).

### Promise / async-queue
```ts
async function* processQueue(items: Item[]) {
  for (const item of items) yield await process(item);
}
```

## Anti-Patterns to Avoid

- **God class** — does everything.
- **Singleton everywhere** — global state hell.
- **Callback hell** — use async/await.
- **Deep inheritance** — composition > inheritance.
- **Premature abstraction** — DRY taken too far.
- **Pattern cargo-culting** — pattern without need.

→ [ANTI-PATTERNS.md](../ANTI-PATTERNS.md)

## References

- Refactoring Guru: https://refactoring.guru/design-patterns
- Addy Osmani's Patterns: https://addyosmani.com/resources/essentialjsdesignpatterns/book/
- Head First Design Patterns
- SourceMaking: https://sourcemaking.com/design_patterns

## Further Reading

- *Design Patterns* — GoF
- *Head First Design Patterns* — friendlier intro
- *Refactoring* — Martin Fowler

## Exercises

1. Implement Observer, Strategy, and Command from scratch.
2. Take a God class in your codebase. Split it using Strategy + Facade.
3. Add undo/redo to a form using Command.

## Projects

- Build a plugin system using Strategy + Factory.
- Build a reactive form library using Observer + BehaviorSubject.

---

**Previous:** [Animations/](../Animations/) · **Next:** [UI/](../UI/) · **Related:** [Clean-Code/](../Clean-Code/), [Architecture/](../Architecture/)
