# Clean Code

> SOLID, naming, refactoring. The code-level craft.

---

## Purpose

Write code that humans (including future you) can read and maintain.

## Prerequisites

- Programming experience.

## Learning Outcome

You can write clean code, refactor safely, and review others' code constructively.

## Dependencies

- A programming language.

## Related Files

- [Architecture/](../Architecture/) · [Design-Patterns/](../Design-Patterns/) · [ANTI-PATTERNS.md](../ANTI-PATTERNS.md) · [COMMON_MISTAKES.md](../COMMON_MISTAKES.md) · [Clean-Code/solid.md](solid.md) · [Clean-Code/srp.md](srp.md)

## AI Instructions

When writing code:
1. **Name things well.** Spend more time than you think.
2. **Small functions** (10-30 lines, one purpose).
3. **Small classes** (one responsibility).
4. **No magic numbers** (use named constants).
5. **No comments that explain WHAT** — code should be self-explanatory. Comments explain WHY.
6. **Pure functions** where possible.
7. **Don't Repeat Yourself** (but don't over-DRY either).
8. **Fail fast.** Validate at boundaries.
9. **Refactor** when code smells.

## Human Notes

### SOLID
- **S**ingle Responsibility — one reason to change.
- **O**pen/Closed — open for extension, closed for modification.
- **L**iskov Substitution — subtypes substitutable for base types.
- **I**nterface Segregation — many specific interfaces > one big.
- **D**ependency Inversion — depend on abstractions.

→ [Clean-Code/solid.md](solid.md)

### Naming
- **Variables**: nouns (`user`, `address`).
- **Functions**: verbs (`getUser`, `sendEmail`).
- **Booleans**: is/has/can/should (`isActive`, `hasPermission`).
- **Constants**: SCREAMING_SNAKE (`MAX_RETRY`).
- **Classes**: PascalCase (`UserController`).
- **Avoid**: `data`, `info`, `temp`, `util`, `helper`. Be specific.

Bad: `const d = new Date();`
Good: `const createdAt = new Date();`

Bad: `function process(x) { ... }`
Good: `function validateEmail(email) { ... }`

### Functions
- Small (10-30 lines).
- Do one thing.
- Few arguments (≤3 ideal).
- No side effects (when possible).
- No flag arguments (split into two functions).
- Return early (guard clauses).

```js
// BAD
function getActiveUsers(users) {
  const result = [];
  for (const u of users) {
    if (u.active) {
      result.push(u);
    }
  }
  return result;
}

// GOOD
const getActiveUsers = (users) => users.filter(u => u.active);
```

### Comments
- Don't comment WHAT (code shows that).
- Comment WHY.
- Comment external references ("OWASP recommendation: ...").
- Comment non-obvious decisions.
- Remove commented-out code.

### Refactoring
When you see a smell:
- Long function → extract.
- Large class → split.
- Duplicate → extract.
- Long param list → parameter object.
- Feature envy → move method.
- Data class → add behavior.

→ [Design-Patterns/](../Design-Patterns/)

### Code smells
- Long method.
- Large class.
- Long parameter list.
- Duplicated code.
- Divergent change.
- Shotgun surgery.
- Feature envy.
- Data class.
- Primitive obsession.
- Switch statements.
- Parallel hierarchies.
- Lazy class.
- Speculative generality.
- Temporary field.
- Message chain.
- Middle man.
- Inappropriate intimacy.
- Alternative classes with different interfaces.
- Incomplete library class.
- Data class.
- Refused bequest.
- Comments.

### Testing
Clean code is testable code.
- Pure functions: easy to test.
- Side effects: harder, mock.
- Coupled code: untestable.

### Code review
- Review for clarity, correctness, security, performance, accessibility.
- Be kind. Suggest, don't dictate.
- Praise good code.

## Common Mistakes

- ❌ Vague names.
- ❌ Long functions.
- ❌ Deeply nested conditionals.
- ❌ Magic numbers.
- ❌ Comments explaining WHAT.
- ❌ Dead code.
- ❌ Premature abstraction.
- ❌ YAGNI violations.
- ❌ Inconsistent style (use formatter).

## Tools

- ESLint, Biome, Prettier.
- SonarQube.
- CodeClimate.

## References

- Clean Code (book): https://www.oreilly.com/library/view/clean-code/9780136083238/
- Refactoring (book): https://refactoring.com/
- Code Smells: https://refactoring.guru/refactoring/smells

## Further Reading

- *Clean Code* — Robert C. Martin (read critically)
- *Refactoring* — Martin Fowler
- *A Philosophy of Software Design* — John Ousterhout
- *The Pragmatic Programmer* — Hunt & Thomas

## Exercises

1. Take a 100-line function. Refactor to ≤20 lines each.
2. Rename vague variables in a file.
3. Remove all comments that explain WHAT.

## Projects

- Refactor a legacy module with tests as safety net.

---

**Previous:** [Security/](../Security/) · **Next:** [System-Design/](../System-Design/) · **Related:** [Architecture/](../Architecture/)
