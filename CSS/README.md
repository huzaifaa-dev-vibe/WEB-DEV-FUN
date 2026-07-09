# CSS

> The styling layer of the web. From selectors to design tokens to layout to animation.

---

## Purpose

Master CSS as a system: selectors, the box model, layout (Flexbox + Grid), responsive design, design tokens, animations, and CSS architecture.

## Prerequisites

- [HTML/](../HTML/)

## Learning Outcome

You can build any layout, theme any app, and write CSS that scales.

## Dependencies

- HTML knowledge.

## Related Files

- [Flexbox/](../Flexbox/) · [Grid/](../Grid/) · [Responsive-Design/](../Responsive-Design/) · [Animations/](../Animations/) · [Typography/](../Typography/) · [Color-Palettes/](../Color-Palettes/) · [ANTI-AI-DESIGN/](../ANTI-AI-DESIGN/) · [CSS/cheat-sheet.md](cheat-sheet.md) · [CSS/best-practices.md](best-practices.md)

## AI Instructions

When writing CSS:
1. **No hard-coded values.** Use tokens (CSS variables).
2. **No `!important`.** Increase specificity naturally or use layers.
3. **Mobile-first.** `min-width` media queries.
4. **Use Flexbox for 1D, Grid for 2D.** Don't fight the wrong tool.
5. **Animate `transform` and `opacity` only.** Never `width`/`height`/`top`/`left`.
6. **Use modern CSS.** `:has()`, container queries, `@layer`, nesting, `clamp()`, `min()`/`max()`.
7. **Pick a styling solution**: Tailwind (default) or CSS Modules or vanilla-extract. Don't mix.
8. **Use `100dvh` not `100vh` on mobile.**
9. **Respect `prefers-reduced-motion`.**
10. **Test in 375px viewport.**

## Human Notes

CSS went through a renaissance. Modern CSS is genuinely good. Learn the new features:

- **CSS Nesting** — no preprocessor needed.
- **`:has()`** — parent selector.
- **Container queries** — component-level responsive.
- **`@layer`** — manage specificity.
- **`@scope`** — scoped styles.
- **`clamp()`, `min()`, `max()`** — fluid sizing.
- **`100dvh`, `100svh`, `100lvh`** — mobile-safe viewport units.
- **`color-mix()`** — blend colors at runtime.
- **OKLCH** — perceptually uniform color space.
- **Subgrid** — Grid children aligned to parent grid.
- **View Transitions API** — page transitions natively.
- **Scroll-driven animations** — CSS only.
- **`anchor-name` / `anchor-pos`** — anchored positioning (where supported).

## The Cascade

Specificity order (low → high):
1. Source order
2. `!important` (avoid)
3. Inline styles
4. IDs
5. Classes, attributes, pseudo-classes
6. Elements, pseudo-elements
7. Universal (`*`)

Use `@layer` to manage:
```css
@layer reset, base, components, utilities;

@layer reset {
  * { box-sizing: border-box; margin: 0; }
}

@layer base {
  body { font-family: var(--font-sans); }
}

@layer components {
  .button { /* ... */ }
}

@layer utilities {
  .text-center { text-align: center; }
}
```

## Box Model

```css
* { box-sizing: border-box; }
```
Always. Every project. First line of CSS.

Box model: content → padding → border → margin.

`width` is content-only by default. With `border-box`, it includes padding + border. Sanity-saving.

## Layout: Flexbox vs Grid

**Flexbox** — 1D (row OR column).
- Nav bars, button groups, card rows, alignment.
- `display: flex; gap: 1rem; align-items: center;`

**Grid** — 2D (rows AND columns).
- Page layout, complex card grids, dashboards.
- `display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));`

See [Flexbox/](../Flexbox/) and [Grid/](../Grid/) for deep dives.

## Design Tokens

```css
:root {
  /* Colors */
  --color-bg: #ffffff;
  --color-fg: #0a0a0a;
  --color-muted: #666666;
  --color-accent: oklch(0.6 0.2 250);
  --color-border: rgb(0 0 0 / 0.1);

  /* Spacing (4px base) */
  --space-1: 0.25rem;
  --space-2: 0.5rem;
  --space-3: 0.75rem;
  --space-4: 1rem;
  --space-6: 1.5rem;
  --space-8: 2rem;
  --space-12: 3rem;
  --space-16: 4rem;
  --space-24: 6rem;

  /* Typography */
  --font-sans: 'Inter', system-ui, sans-serif;
  --font-mono: 'JetBrains Mono', ui-monospace, monospace;
  --text-xs: 0.75rem;
  --text-sm: 0.875rem;
  --text-base: 1rem;
  --text-lg: 1.125rem;
  --text-xl: 1.25rem;
  --text-2xl: 1.5rem;
  --text-3xl: 1.875rem;
  --text-4xl: 2.25rem;

  /* Radius */
  --radius-sm: 0.25rem;
  --radius: 0.5rem;
  --radius-lg: 1rem;
  --radius-full: 9999px;

  /* Shadow */
  --shadow-sm: 0 1px 2px rgb(0 0 0 / 0.05);
  --shadow: 0 1px 3px rgb(0 0 0 / 0.1), 0 1px 2px rgb(0 0 0 / 0.06);
  --shadow-lg: 0 10px 15px -3px rgb(0 0 0 / 0.1);

  /* Z-index */
  --z-base: 0;
  --z-dropdown: 1000;
  --z-sticky: 1100;
  --z-modal: 1300;
  --z-toast: 1400;

  /* Motion */
  --duration-fast: 150ms;
  --duration: 200ms;
  --duration-slow: 400ms;
  --ease: cubic-bezier(0.4, 0, 0.2, 1);
}

@media (prefers-color-scheme: dark) {
  :root {
    --color-bg: #0a0a0a;
    --color-fg: #fafafa;
    --color-muted: #a0a0a0;
    --color-border: rgb(255 255 255 / 0.1);
  }
}
```

→ See [CSS/variables.md](variables.md) for deeper token guidance.

## Responsive Design (mobile-first)

```css
/* Mobile-first: base styles are for mobile */
.card {
  padding: var(--space-4);
  font-size: var(--text-base);
}

/* Tablet+ */
@media (min-width: 768px) {
  .card {
    padding: var(--space-6);
    font-size: var(--text-lg);
  }
}

/* Desktop+ */
@media (min-width: 1024px) {
  .card {
    padding: var(--space-8);
  }
}

/* Fluid type */
h1 {
  font-size: clamp(2rem, 5vw, 4rem);
}
```

→ [Responsive-Design/](../Responsive-Design/)

## Container Queries

```css
.card-container {
  container-type: inline-size;
  container-name: card;
}

@container card (min-width: 400px) {
  .card {
    grid-template-columns: 1fr 2fr;
  }
}
```

## Modern Selectors

```css
/* :has() — parent selector */
.card:has(img) { padding-top: 0; }
form:has(input:invalid) button { opacity: 0.5; }

/* :is() / :where() — group selectors */
:where(h1, h2, h3) { color: var(--color-fg); } /* :where has 0 specificity */

/* :not() */
nav a:not([aria-current]) { color: var(--color-muted); }

/* Nested */
.card {
  padding: 1rem;
  & .title { font-size: 1.5rem; }
  &:hover { transform: translateY(-2px); }
}
```

## Animations

```css
.fade-in {
  animation: fadeIn var(--duration) var(--ease);
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(8px); }
  to { opacity: 1; transform: translateY(0); }
}

@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

→ [Animations/](../Animations/)

## Tailwind

For new projects, Tailwind is the default. v4 is even faster (no PostCSS, Lightning CSS under the hood).

```html
<button class="bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded-md transition-colors">
  Click me
</button>
```

→ [CSS/tailwind.md](tailwind.md) for deep dive.

## CSS Architecture

For non-Tailwind projects:
- **BEM** — `.block__element--modifier`.
- **CSS Modules** — scoped class names.
- **CSS-in-JS** (vanilla-extract, Panda) — build-time extraction.
- **Utility-first** (Tailwind, UnoCSS).

Pick ONE per project.

→ [CSS/architecture.md](architecture.md)

## Common Mistakes

→ [COMMON_MISTAKES.md#css](../COMMON_MISTAKES.md)

Highlights:
- `!important` everywhere.
- Magic numbers.
- Hard-coded colors.
- `position: absolute` for layout.
- Animations on layout properties.
- `z-index: 999999`.

## References

- MDN CSS: https://developer.mozilla.org/en-US/docs/Web/CSS
- CSS Spec (W3C): https://www.w3.org/Style/CSS/
- CSS Tricks: https://css-tricks.com/
- web.dev CSS: https://web.dev/learn/css
- Kevin Powell YouTube: https://www.youtube.com/kepowob
- CSS-Tricks Almanac: https://css-tricks.com/almanac/
- Can I Use: https://caniuse.com/

## Further Reading

- *CSS Secrets* — Lea Verou
- *Every Layout* — Heydon Pickering, Andy Bell (https://every-layout.dev/)
- *Refactoring UI* — Adam Wathan & Steve Schoger
- *Practical Typography* — Matthew Butterick

## Exercises

1. Build a card grid that reflows 3→2→1 columns based on viewport.
2. Implement a navbar with Flexbox, no JS.
3. Use container queries to make a component adapt to its container.
4. Build a dark mode toggle using only CSS variables + `prefers-color-scheme`.
5. Recreate a layout from Awwwards using only HTML + CSS.

## Projects

- Build a design system token set + 5 components.
- Build a fully responsive dashboard layout (sidebar + main + header).
- Build a 3D card hover effect with `transform-style: preserve-3d`.

---

**Previous:** [HTML/](../HTML/) · **Next:** [JavaScript/](../JavaScript/) · **Related:** [Flexbox/](../Flexbox/), [Grid/](../Grid/), [Animations/](../Animations/)
