# DESIGN SYSTEM (Overview)

> A design system is the single source of truth for design decisions. Deep coverage in [DESIGN_SYSTEM.md](DESIGN_SYSTEM.md) and [UI/](UI/).

---

## Purpose

Stop re-deciding colors, spacing, typography, and components. Codify them. Ship faster. Stay consistent.

## Prerequisites

- Basic UI/UX understanding.
- CSS fundamentals.

## Learning Outcome

You can design, document, and ship a design system that a team actually uses.

## Related Files

- [UI/](UI/) — components
- [UX/](UX/) — flows & principles
- [Typography/](Typography/) — type
- [Color-Palettes/](Color-Palettes/) — palettes
- [ANTI-AI-DESIGN/](ANTI-AI-DESIGN/) — anti-AI principles
- [CSS/variables.md](CSS/variables.md) — tokens

## AI Instructions

When building UI:
1. Use design tokens (CSS variables). → [CSS/variables.md](CSS/variables.md)
2. Use a spacing scale (4/8/12/16/24/32/48/64/96/128).
3. Use a type scale (12/14/16/18/20/24/30/36/48/60).
4. Use a color palette with intent. → [Color-Palettes/](Color-Palettes/)
5. Use a component library (shadcn/ui default) and customize via tokens.
6. Document decisions in a Storybook or markdown.
7. Don't hard-code values. Tokenize.

## Human Notes

A design system is NOT a component library. It's the *system*: tokens, components, patterns, principles, docs, governance.

### Layers
```
Principles → Tokens → Components → Patterns → Templates → Pages
```

### Tokens
Atomic design decisions as variables:
- **Color**: `--color-bg`, `--color-fg`, `--color-accent`, `--color-muted`, etc.
- **Spacing**: `--space-1` (4px) ... `--space-16` (64px) and beyond.
- **Typography**: `--font-sans`, `--font-mono`, sizes, weights, line-heights.
- **Radius**: `--radius-sm`, `--radius`, `--radius-lg`, `--radius-full`.
- **Shadow**: `--shadow-sm`, `--shadow`, `--shadow-lg`.
- **Z-index**: `--z-dropdown`, `--z-modal`, `--z-toast`.
- **Motion**: `--duration-fast`, `--duration`, `--duration-slow`, `--ease`.

### Components
Built from tokens. Reusable. Documented (props, examples, do/don't).
- Buttons, inputs, selects, checkboxes, radios, switches.
- Cards, dialogs, popovers, tooltips, toasts.
- Tables, lists, menus, tabs, accordions.
- Layout: container, grid, stack, sidebar.

### Patterns
Composed solutions to common UX problems:
- Empty state
- Loading state
- Error state
- Form layout
- List + detail
- Filter + sort
- Pagination

### Principles
Non-negotiable rules. Examples:
- "Default to dark mode support."
- "Every interactive element has a visible focus state."
- "Animation is for explanation, not decoration."
- "Mobile-first always."

### Governance
- Who can add tokens? Components?
- RFC process for changes.
- Versioning (semver).
- Deprecation policy.
- Adoption tracking.

## Tech Stack for a Design System

| Need | Tool |
|---|---|
| Tokens | CSS variables, Style Dictionary, Theo |
| Components | React + Radix + Tailwind (shadcn pattern), Stitches, vanilla-extract |
| Docs | Storybook, Ladle |
| Visual testing | Chromatic, Percy |
| Distribution | npm package, or copy-paste (shadcn pattern) |
| Figma sync | Figma Tokens plugin, Specify, Supernova |

## The shadcn/ui Pattern

Not a library — a *recipe*:
- Copy components into your codebase.
- Customize freely (no library lock-in).
- Built on Radix primitives + Tailwind.
- Tokens via Tailwind config + CSS variables.

→ [EXTERNAL_REPOSITORIES.md](EXTERNAL_REPOSITORIES.md#component-libraries)

## Anti-patterns

- **No tokens.** Hard-coded values everywhere.
- **Tokens for everything.** 200 colors nobody uses.
- **Documentation in a separate tool nobody opens.**
- **Components that wrap library X with no value-add.**
- **Governance so heavy nobody ships.**
- **No deprecation path.**

## References

- https://www.designsystems.com/
- https://www.invisionapp.com/inside-design/design-systems/
- https://designsystemsrepo.com/
- https://danprocida.com/writing-on-design-systems/
- Brad Frost: https://brad-frost.com/
- Nathan Curtis: https://medium.com/@nathanacurtis

## Further Reading

- *Atomic Design* — Brad Frost (free)
- *Design Systems* — Alla Kholmatova
- *Modular Web Design* — Nathan Curtis
- *Refactoring UI* — Adam Wathan & Steve Schoger

## Exercises

1. Audit your current project. Find every hard-coded color/spacing/font-size. Replace with tokens.
2. Pick a small app. Build it without any component library — just tokens.
3. Document one component as if it were in a design system (props, examples, do/don't).

## Projects

- Build a design system from scratch for a SaaS dashboard.
- Set up Storybook with visual regression testing.

---

**Next:** [UI/](UI/) · [ANTI-AI-DESIGN/](ANTI-AI-DESIGN/) · [Color-Palettes/](Color-Palettes/)
