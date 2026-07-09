# SVG

> Scalable Vector Graphics. Crisp at any size, scriptable, animatable, small.

---

## Purpose

Master SVG: inline, sprite, animation, optimization, accessibility.

## Prerequisites

- [HTML/](../HTML/), [CSS/](../CSS/).

## Learning Outcome

You can use SVG effectively for icons, illustrations, data viz, and animation.

## Dependencies

- Browser (everywhere).

## Related Files

- [Icons/](../Icons/) · [Illustrations/](../Illustrations/) · [Canvas/](../Canvas/) · [Animations/](../Animations/)

## AI Instructions

When using SVG:
1. **Inline** for icons and small graphics (control via CSS).
2. **`<img>`** for standalone illustrations.
3. **Sprite + `<use>`** for many icons (legacy but valid).
4. **Optimize** with SVGO before shipping.
5. **Make accessible**: `<title>`, `<desc>`, `role="img"`, `aria-label`.
6. **Decorative SVGs**: `aria-hidden="true"`.

## Human Notes

### SVG basics
```html
<svg width="100" height="100" viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" fill="blue" />
  <rect x="10" y="10" width="80" height="80" stroke="black" fill="none" />
  <line x1="0" y1="0" x2="100" y2="100" stroke="red" />
  <path d="M10 10 L 90 10 L 50 90 Z" fill="green" />
  <text x="50" y="50" text-anchor="middle">Hello</text>
</svg>
```

### Inline vs img vs sprite
- **Inline** — best for icons. CSS controls color (`currentColor`). Animatable.
- **`<img src="x.svg">`** — best for standalone illustrations. Can't style with CSS.
- **Sprite + `<use>`** — many icons, one file. Cachable. Harder to color individually.
- **CSS `background: url(x.svg)`** — decorative only.

### `currentColor` for theming
```html
<svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
  <path d="..." />
</svg>
```
Color via CSS: `color: var(--color-accent);`.

### Accessibility
```html
<svg role="img" aria-label="Chart of sales by month">
  <title>Sales by month</title>
  <desc>Bar chart showing sales from January to December 2024.</desc>
  <!-- ... -->
</svg>

<!-- OR decorative -->
<svg aria-hidden="true" focusable="false">...</svg>
```

### Animation
```css
.spin { animation: spin 1s linear infinite; }
@keyframes spin {
  to { transform: rotate(360deg); }
}
```

For complex SVG animation: GSAP, Lottie, or SMIL (deprecated but works).

### Optimization
- Run SVGO: https://github.com/svg/svgo
- Or SVGOMG (web): https://jakearchibald.github.io/svgomg/
- Strips metadata, comments, unused attrs. Often 30-50% smaller.

### Responsive SVG
```html
<svg viewBox="0 0 100 100" style="width: 100%; height: auto;">
  <!-- preserves aspect ratio, scales with container -->
</svg>
```

### SVG as data viz
For complex data viz, use D3 or a charting library (Recharts, etc.). Don't hand-roll.

## Common Mistakes

- ❌ Embedded base64 SVG (use inline or external file).
- ❌ No `viewBox`.
- ❌ Fixed `width`/`height` on responsive SVGs.
- ❌ Inkscape metadata bloat (run SVGO).
- ❌ No accessibility (`<title>`, `aria-hidden`).
- ❌ Trying to animate complex SVGs without a library.

## Tools

- SVGO: https://github.com/svg/svgo
- SVGOMG: https://jakearchibald.github.io/svgomg/
- SVG Editor: https://svgedit.netlify.app/
- Figma (export to SVG)
- Inkscape (open-source editor)

## References

- MDN SVG: https://developer.mozilla.org/en-US/docs/Web/SVG
- SVG on the web: https://svgontheweb.com/
- Sara Soueidan's blog: https://www.sarasoueidan.com/blog/

## Further Reading

- *Practical SVG* — Chris Coyier
- *Using SVG with CSS3 and HTML5* — Amelia Bellamy-Royds

## Exercises

1. Inline an SVG icon. Style it with CSS.
2. Build a small SVG illustration and animate one element.
3. Run SVGOMG on a Figma-exported SVG. Compare sizes.

## Projects

- Build an animated SVG hero illustration.
- Build a simple SVG chart by hand.

---

**Previous:** [Illustrations/](../Illustrations/) · **Next:** [Canvas/](../Canvas/) · **Related:** [Icons/](../Icons/)
