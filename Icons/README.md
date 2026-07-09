# Icons

> SVG icons. Not emoji. Not fonts.

---

## Purpose

Build a coherent icon system using SVG, with size and stroke consistency.

## Prerequisites

- [HTML/](../HTML/), [SVG/](../SVG/).

## Learning Outcome

You can pick, install, customize, and ship a consistent icon system.

## Dependencies

- SVG support (everywhere).

## Related Files

- [SVG/](../SVG/) · [UI/](../UI/) · [EXTERNAL_REPOSITORIES.md#icons](../EXTERNAL_REPOSITORIES.md#icons)

## AI Instructions

When using icons:
1. **Pick one icon set** (default: Lucide).
2. **Don't mix sets** (different strokes/sizes look bad).
3. **Use SVG, not fonts.**
4. **Size via `width`/`height` or `font-size` + `1em`.**
5. **Color via `currentColor`.**
6. **Always include `aria-label` or `aria-hidden="true"`** for icon-only buttons.

## Human Notes

### Icon sets
- **Lucide** — default. Clean, 24×24, 2px stroke. https://lucide.dev
- **Phosphor** — multiple weights. https://phosphoricons.com
- **Heroicons** — Tailwind team. https://heroicons.com
- **Tabler** — 5000+ icons. https://tabler.io/icons
- **Iconify** — 200k+ icons, on-demand. https://icon-sets.iconify.design
- **Material Symbols** — Google. https://fonts.google.com/icons
- **Bootstrap Icons** — https://icons.getbootstrap.com

### Approach
- **Per-icon import** (best for tree-shaking): `import { Check } from 'lucide-react'`.
- **Icon font** (avoid): hard to style, no individual control.
- **Sprite** (legacy): one HTTP request, harder to customize.

### SVG icon component
```jsx
function Icon({ name, size = 24, className }) {
  const paths = { check: 'M20 6L9 17l-5-5', x: 'M18 6L6 18M6 6l12 12' };
  return (
    <svg
      width={size}
      height={size}
      viewBox="0 0 24 24"
      fill="none"
      stroke="currentColor"
      strokeWidth="2"
      strokeLinecap="round"
      strokeLinejoin="round"
      className={className}
      aria-hidden="true"
    >
      <path d={paths[name]} />
    </svg>
  );
}
```

### Icon-only buttons (a11y)
```jsx
<button aria-label="Close">
  <Icon name="x" />
</button>
```

### Sizing with CSS
```css
.icon { width: 1em; height: 1em; }
.text-lg .icon { width: 1.25em; height: 1.25em; }
```

### Coloring
```css
.icon { color: currentColor; }
button:hover .icon { color: var(--color-accent); }
```

## Common Mistakes

- ❌ Emoji as icons.
- ❌ Mixing icon sets.
- ❌ Different stroke widths.
- ❌ Inconsistent sizes.
- ❌ No `aria-label` on icon-only buttons.
- ❌ Icon fonts (hard to style, render issues).

## Tools

- SVGO: https://github.com/svg/svgo
- SVGOMG: https://jakearchibald.github.io/svgomg/
- IcoMoon: https://icomoon.io/

## References

- Lucide: https://lucide.dev
- Iconify: https://icon-sets.iconify.design

## Exercises

1. Set up a tree-shakeable icon system in your app.
2. Build an icon-only button with proper a11y.

## Projects

- Build a custom icon set for your brand.

---

**Previous:** [Typography/](../Typography/) · **Next:** [Illustrations/](../Illustrations/) · **Related:** [SVG/](../SVG/), [UI/](../UI/)
