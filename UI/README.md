# UI

> Components, kits, patterns, design systems. The building blocks of interfaces.

---

## Purpose

Master the components, libraries, and patterns that make up modern UIs. Build a coherent design system.

## Prerequisites

- [HTML/](../HTML/), [CSS/](../CSS/), [JavaScript/](../JavaScript/), [Accessibility/](../Accessibility/).

## Learning Outcome

You can build, choose, and compose UI components into coherent interfaces.

## Dependencies

- A frontend framework (React/Vue/Svelte/Angular).

## Related Files

- [UX/](../UX/) · [Typography/](../Typography/) · [Color-Palettes/](../Color-Palettes/) · [Icons/](../Icons/) · [ANTI-AI-DESIGN/](../ANTI-AI-DESIGN/) · [DESIGN_SYSTEM.md](../DESIGN_SYSTEM.md) · [EXTERNAL_REPOSITORIES.md#component-libraries](../EXTERNAL_REPOSITORIES.md#component-libraries)

## AI Instructions

When building UI:
1. **Pick a component library** (default: shadcn/ui for React). → [EXTERNAL_REPOSITORIES.md](../EXTERNAL_REPOSITORIES.md#component-libraries)
2. **Customize via tokens**, not by editing components.
3. **Don't reinvent components** that exist (modals, dropdowns, etc.).
4. **Build accessibly** from the start. → [Accessibility/](../Accessibility/)
5. **Don't look AI-generated.** → [ANTI-AI-DESIGN/](../ANTI-AI-DESIGN/)
6. **Document each component** (props, examples, do/don't).
7. **Storybook** for component dev.
8. **Co-locate component + test + story.**

## Human Notes

### Component categories
- **Primitives** — Button, Input, Select, Checkbox, Radio, Switch, Textarea.
- **Layout** — Container, Stack, Grid, Card, Sidebar, Header, Footer.
- **Navigation** — Tabs, Breadcrumb, Pagination, Menu, Nav.
- **Overlay** — Modal, Popover, Tooltip, Toast, Drawer.
- **Data display** — Table, List, Badge, Avatar, Tag, Chip.
- **Feedback** — Alert, Progress, Spinner, Skeleton.
- **Form patterns** — Form, Field, Fieldset, Errors.

### Component libraries (default picks)
- **React:** shadcn/ui (Radix + Tailwind), Mantine, Chakra UI, MUI.
- **Vue:** shadcn-vue, Reka UI, PrimeVue, Vuetify, Nuxt UI.
- **Svelte:** shadcn-svelte, Melt UI, Skeleton.
- **Angular:** Angular Material, PrimeNG, NG-Zorro.

→ [EXTERNAL_REPOSITORIES.md](../EXTERNAL_REPOSITORIES.md#component-libraries)

### Component anatomy
A good component:
- Has clear props (typed, documented).
- Composes (via `asChild`/`as`, slots, render props).
- Is accessible by default.
- Has sensible defaults.
- Is themeable via tokens.
- Has loading, error, empty states (for data components).
- Has tests (render, interaction, a11y).
- Has a Storybook story.

### Component-first thinking
Don't build "pages". Build components. Compose components into pages.

### Pattern: Compound Components
```jsx
<Card>
  <Card.Header>
    <Card.Title>...</Card.Title>
    <Card.Action>...</Card.Action>
  </Card.Header>
  <Card.Body>...</Card.Body>
  <Card.Footer>...</Card.Footer>
</Card>
```

### Pattern: Slots
```jsx
<Dialog>
  <Dialog.Trigger asChild>
    <Button>Open</Button>
  </Dialog.Trigger>
  <Dialog.Content>
    <Dialog.Title>...</Dialog.Title>
    <Dialog.Description>...</Dialog.Description>
  </Dialog.Content>
</Dialog>
```

### Pattern: Polymorphic (`as` / `asChild`)
```jsx
<Button asChild>
  <a href="/login">Log in</a>
</Button>
// Renders an <a> with button styles
```

## Common Patterns

### Empty state
- Explain what's missing.
- Suggest a next action.
- Use illustration if appropriate.

### Loading state
- Skeleton for known shapes.
- Spinner for unknown.
- Inline progress for known totals.

### Error state
- Explain what went wrong.
- Suggest a fix or retry.
- Don't show stack traces to users.

### Forms
- One column on mobile.
- Labels above inputs.
- Helpers below inputs.
- Errors below inputs, in red.
- Required indicators (asterisk or text).
- Submit button at end.
- Disabled until valid? Or allow submit and show errors? (Debate.)

### Lists
- Virtualize long lists.
- Use `role="list"` if non-native.
- Empty state.

### Tables
- Sticky header.
- Sortable columns (with aria).
- Pagination or virtualization.
- Responsive: stack to cards on mobile.

### Modals
- Focus trap.
- Return focus on close.
- Esc to close.
- Backdrop click to close.
- Body scroll lock.

## Common Mistakes

- ❌ Reinventing modal/dropdown/etc.
- ❌ Building components without accessibility.
- ❌ Hard-coded values instead of tokens.
- ❌ No empty/loading/error states.
- ❌ Generic AI-looking components. → [ANTI-AI-DESIGN/](../ANTI-AI-DESIGN/)
- ❌ No tests.
- ❌ No docs.

## Tools

- Storybook: https://storybook.js.org/
- Ladle (lighter): https://ladle.dev/
- Bit: https://bit.dev/
- Figma: design before code.

## References

- Refactoring UI: https://www.refactoringui.com/
- Material Design 3: https://m3.material.io/
- Apple HIG: https://developer.apple.com/design/human-interface-guidelines/
- Polaris (Shopify): https://polaris.shopify.com/
- Lightning Design System (Salesforce): https://www.lightningdesignsystem.com/
- Carbon (IBM): https://carbondesignsystem.com/

## Further Reading

- *Atomic Design* — Brad Frost (free)
- *Designing Web Interfaces* — Bill Scott, Theresa Neil
- *Refactoring UI* — Adam Wathan & Steve Schoger

## Exercises

1. Build a Card component (header, body, footer slots).
2. Build a Modal with focus trap, Esc, backdrop click.
3. Build a Tabs component with keyboard nav.
4. Build a Table with sortable columns.

## Projects

- Build a design system from scratch (10+ components, tokens, Storybook).
- Build a dashboard layout with sidebar, header, and main grid.

---

**Previous:** [Design-Patterns/](../Design-Patterns/) · **Next:** [UX/](../UX/) · **Related:** [ANTI-AI-DESIGN/](../ANTI-AI-DESIGN/)
