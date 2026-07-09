# TypeScript

> JavaScript with types. The default for new projects of any size.

---

## Purpose

Add static types to JavaScript. Catch bugs at compile time. Get better tooling. Scale codebases.

## Prerequisites

- Solid [JavaScript/](../JavaScript/).

## Learning Outcome

You can read, write, and design TypeScript types. Configure tsconfig. Use generics, narrowing, and utility types. Avoid `any`.

## Dependencies

- Node.js / Bun / Deno.

## Related Files

- [JavaScript/](../JavaScript/) · [TypeScript/cheat-sheet.md](cheat-sheet.md) · [TypeScript/generics.md](generics.md) · [TypeScript/tsconfig.md](tsconfig.md)

## AI Instructions

When writing TS:
1. **No `any` without a comment.** Use `unknown` + narrowing.
2. **Strict mode on.** `"strict": true` in tsconfig.
3. **Don't trust `as`.** Use type guards.
4. **Validate at boundaries.** Zod for runtime, TS for compile time.
5. **Use `satisfies` over `as` where possible.**
6. **Use `unknown` for any untrusted input.**
7. **Don't annotate what TS can infer.**
8. **Use the right utility type** (`Pick`, `Omit`, `Partial`, `Required`, `Readonly`, `Record`, `ReturnType`, `Parameters`, `Awaited`).
9. **Generics over `any`.**
10. **Run `tsc --noEmit` in CI.**

## Human Notes

TypeScript is structural (duck-typed), not nominal. This is powerful but takes getting used to.

Key concepts:
- **Inference** — TS infers types; you don't always have to annotate.
- **Narrowing** — `typeof`, `instanceof`, `in`, discriminated unions.
- **Generics** — reusable, type-safe code.
- **Structural typing** — if it has the right shape, it fits.
- **Excess property checks** — only on object literals.
- **Declaration files** (`.d.ts`) — describe JS libraries to TS.

## tsconfig.json (recommended)

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "ESNext",
    "moduleResolution": "Bundler",
    "lib": ["ES2022", "DOM", "DOM.Iterable"],
    "strict": true,
    "noUncheckedIndexedAccess": true,
    "noImplicitOverride": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noFallthroughCasesInSwitch": true,
    "exactOptionalPropertyTypes": true,
    "verbatimModuleSyntax": true,
    "isolatedModules": true,
    "skipLibCheck": true,
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "resolveJsonModule": true,
    "jsx": "preserve",
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    },
    "noEmit": true
  },
  "include": ["src"]
}
```

→ [TypeScript/tsconfig.md](tsconfig.md) for option-by-option explanation.

## Basic Types

```typescript
// Primitives
let str: string = 'hello';
let num: number = 42;
let bool: boolean = true;
let n: null = null;
let u: undefined = undefined;
let big: bigint = 100n;
let sym: symbol = Symbol();

// Arrays
let nums: number[] = [1, 2, 3];
let strs: Array<string> = ['a', 'b'];

// Tuples (fixed length, fixed types)
let pair: [string, number] = ['a', 1];

// Literals
let direction: 'left' | 'right' = 'left';
let dice: 1 | 2 | 3 | 4 | 5 | 6 = 4;

// any / unknown / never
let anything: any = 'safe to do anything'; // AVOID
let unknown: unknown = 'must narrow first'; // PREFER over any
let never: never; // unreachable

// void (function returns nothing)
function log(msg: string): void { console.log(msg); }
```

## Interfaces vs Types

```typescript
// Interface — extendable, declaration-merged
interface User {
  id: string;
  name: string;
  email?: string; // optional
  readonly role: string; // immutable
}

interface User {
  age?: number; // merged with above
}

// Type alias — more flexible (unions, intersections, primitives)
type Status = 'active' | 'inactive';
type ID = string | number;
type UserWithStatus = User & { status: Status };
```

Rule of thumb: `interface` for objects, `type` for unions/primitives.

## Functions

```typescript
// Named
function add(a: number, b: number): number { return a + b; }

// Arrow
const add = (a: number, b: number): number => a + b;

// Optional + default + rest
function greet(name: string, greeting?: string, ...extras: string[]): string {
  return `${greeting ?? 'Hello'}, ${name}! ${extras.join(' ')}`;
}

// Function type
type Callback = (error: Error | null, data?: unknown) => void;

// Overloads
function parse(input: string): object;
function parse(input: string, schema: 'array'): unknown[];
function parse(input: string, schema?: 'array'): object | unknown[] {
  // implementation
}
```

## Generics

```typescript
function first<T>(arr: T[]): T | undefined { return arr[0]; }
const n = first([1, 2, 3]); // number | undefined

function pair<A, B>(a: A, b: B): [A, B] { return [a, b]; }

// Constrained
function getLength<T extends { length: number }>(x: T): number { return x.length; }

// Default
function create<T = string>(): T[] { return []; }

// Inference
const result = first(['a', 'b']); // string | undefined
```

→ [TypeScript/generics.md](generics.md) for deep dive.

## Narrowing

```typescript
function handle(x: string | number | null) {
  if (x === null) return;
  if (typeof x === 'string') return x.toUpperCase();
  return x.toFixed(2);
}

// instanceof
class NetworkError extends Error {}
if (err instanceof NetworkError) { /* ... */ }

// in
interface Cat { meow(): void }
interface Dog { bark(): void }
function speak(animal: Cat | Dog) {
  if ('meow' in animal) animal.meow();
  else animal.bark();
}

// Discriminated unions
type Result = { ok: true; value: string } | { ok: false; error: string };
function handle(r: Result) {
  if (r.ok) return r.value;
  return r.error;
}

// Type predicates
function isString(x: unknown): x is string {
  return typeof x === 'string';
}
```

## Utility Types

```typescript
interface User { id: string; name: string; email?: string; role: string; }

type PartialUser = Partial<User>;          // all optional
type RequiredUser = Required<User>;        // all required
type ReadonlyUser = Readonly<User>;        // all readonly
type PickUser = Pick<User, 'id' | 'name'>; // only id, name
type OmitUser = Omit<User, 'role'>;        // all but role
type UserRecord = Record<string, User>;    // { [k: string]: User }
type UserValues = User[keyof User];        // string | undefined
type UserName = Pick<User, 'name'>;        // { name: string }
type ReturnTypeOf<T> = T extends (...args: any[]) => infer R ? R : never;
type AwaitedOf<T> = Awaited<T>;            // unwrap Promise
type ParametersOf<T> = Parameters<T>;      // tuple of args
```

## `unknown` over `any`

```typescript
// BAD
function parse(json: string): any { return JSON.parse(json); }
const data = parse(json);
data.foo.bar.baz; // no error, but might crash

// GOOD
function parse(json: string): unknown { return JSON.parse(json); }
const data = parse(json);
// data.foo.bar.baz; // ERROR — must narrow first
if (typeof data === 'object' && data !== null && 'foo' in data) {
  // ...
}

// BEST — use Zod
import { z } from 'zod';
const Schema = z.object({ foo: z.string() });
const parsed = Schema.parse(JSON.parse(json));
parsed.foo.toUpperCase(); // safe
```

## `satisfies` (TS 4.9+)

```typescript
type Routes = 'home' | 'about' | 'contact';

// Without satisfies: config is typed as Record<string, string>, losing the literal types
const config = { home: '/index', about: '/about', contact: '/contact' };

// With satisfies: keeps the literal types AND checks the shape
const config2 = {
  home: '/index',
  about: '/about',
} satisfies Record<Routes, string>;
// ERROR: 'contact' is missing
```

## Enums (preferably union types)

```typescript
// Avoid — runtime object, less tree-shakeable
enum Status { Active, Inactive }

// Prefer — union of string literals
type Status = 'active' | 'inactive';

// Or `as const`
const Status = {
  Active: 'active',
  Inactive: 'inactive',
} as const;
type Status = typeof Status[keyof typeof Status];
```

## Decorators (TS 5.0+)

```typescript
function log(target: any, context: ClassMethodDecoratorContext) {
  return function (...args: any[]) {
    console.log(`Calling ${String(context.name)}`);
    return target.apply(this, args);
  };
}

class Foo {
  @log
  bar() { /* ... */ }
}
```

## Common Mistakes

- ❌ `any` everywhere.
- ❌ `as any` to silence errors.
- ❌ Non-strict tsconfig.
- ❌ `noUncheckedIndexedAccess` not enabled (you'll get `T` instead of `T | undefined` from `arr[i]`).
- ❌ Inventing types when stdlib has them.
- ❌ Type annotations when inference works.

→ [COMMON_MISTAKES.md#javascript--typescript](../COMMON_MISTAKES.md)

## References

- TS Handbook: https://www.typescriptlang.org/docs/handbook/
- TS Deep Dive (Basarat): https://basarat.gitbook.io/typescript/
- Total TypeScript: https://www.totaltypescript.com/
- Matt Pocock's blog: https://www.totaltypescript.com/articles
- TypeScript Playground: https://www.typescriptlang.org/play
- TS Spec: https://github.com/microsoft/TypeScript

## Further Reading

- *Effective TypeScript* — Dan Vanderkam
- *Total TypeScript* (course) — Matt Pocock

## Exercises

1. Convert a JS file to TS with strict mode. No `any`.
2. Implement a `Result<T, E>` type and use it.
3. Build a typed event emitter.
4. Write a generic `GroupBy<T>` utility type.
5. Implement Zod schemas for an API and infer types from them.

## Projects

- Build a typed ORM layer (no `any`).
- Build a typed RPC (tRPC-style) between client and server.
- Convert an existing JS library to TS without breaking the API.

---

**Previous:** [JavaScript/](../JavaScript/) · **Next:** [Accessibility/](../Accessibility/) · **Related:** [NodeJS/](../NodeJS/), [Prisma/](../Prisma/)
