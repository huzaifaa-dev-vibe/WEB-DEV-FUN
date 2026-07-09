# Responsive Design

> One codebase. Every screen. From 320px watches to 4K monitors.

---

## Purpose

Build layouts that adapt gracefully from mobile to ultra-wide. Mobile-first, always.

## Prerequisites

- [CSS/](../CSS/), [Flexbox/](../Flexbox/), [Grid/](../Grid/).

## Learning Outcome

You can ship a layout that looks great at 320px, 1440px, and 2560px, with no horizontal scroll.

## Dependencies

- HTML, CSS.

## Related Files

- [CSS/](../CSS/) · [Flexbox/](../Flexbox/) · [Grid/](../Grid/) · [Responsive-Design/units.md](units.md) · [Responsive-Design/breakpoints.md](breakpoints.md) · [Responsive-Design/container-queries.md](container-queries.md)

## AI Instructions

When building responsive UI:
1. **Mobile-first.** Base styles are mobile. Add `min-width` media queries.
2. **Use `clamp()`** for fluid type.
3. **Use `100dvh`** not `100vh` on mobile.
4. **Container queries** for component-level responsive.
5. **Test at 320px, 768px, 1024px, 1440px** minimum.
6. **No horizontal scroll** at any viewport.
7. **Touch targets ≥ 44×44px**.
8. **Images responsive**: `max-width: 100%; height: auto;` + `srcset`.
9. **Don't hide content on mobile** unless you really mean to.

## Human Notes

### Mobile-first
- Default styles target mobile (smallest screen).
- Progressive enhancement for larger screens.
- Forces simplicity. Catches "we don't need this on mobile" early.

### Breakpoints
Don't target specific devices. Target the design's natural break points.

Common (Tailwind-inspired):
- `sm: 640px` — large phones in landscape.
- `md: 768px` — tablets.
- `lg: 1024px` — laptops.
- `xl: 1280px` — desktops.
- `2xl: 1536px` — large desktops.

But better: find where YOUR design breaks.

```css
/* Mobile-first */
.card {
  padding: 1rem;
  grid-template-columns: 1fr;
}

@media (min-width: 768px) {
  .card {
    padding: 2rem;
    grid-template-columns: 1fr 1fr;
  }
}
```

### Fluid type
```css
h1 {
  font-size: clamp(2rem, 5vw + 1rem, 4rem);
}
```
- Min: 2rem (mobile).
- Max: 4rem (large desktop).
- Fluid in between (5vw + 1rem, linear-ish).

### Viewport units
- `vh` — viewport height. Old, broken on mobile (browser UI overlaps).
- `dvh` — dynamic viewport height. Use this.
- `svh` — small viewport height (when UI shown).
- `lvh` — large viewport height (when UI hidden).
- `vw` — viewport width.
- `cqw` / `cqh` — container query units.

→ [Responsive-Design/units.md](units.md)

### Container queries
Make components adapt to their container, not the viewport:
```css
.card-container {
  container-type: inline-size;
}
@container (min-width: 400px) {
  .card { grid-template-columns: 1fr 2fr; }
}
```

→ [Responsive-Design/container-queries.md](container-queries.md)

### Touch
- Min touch target: 44×44px (Apple) / 48×48dp (Google).
- Don't rely on hover-only interactions.
- Don't fire on touchend without delay (double-tap issue, mostly fixed in modern browsers).

### Images
```html
<img
  src="/hero-800.webp"
  srcset="/hero-400.webp 400w, /hero-800.webp 800w, /hero-1600.webp 1600w"
  sizes="(max-width: 600px) 100vw, 50vw"
  alt="..."
  width="800"
  height="600"
  loading="lazy"
  decoding="async"
>
```

→ [Performance/images.md](../Performance/images.md)

### Tables
- Horizontal scroll on small screens: `overflow-x: auto`.
- Or use CSS to transform into stacked cards.

### Navigation
- Hamburger menu on mobile.
- Drawer / sheet pattern.
- Bottom tab bar (mobile-first apps).

## Common Mistakes

- ❌ Desktop-first (uses `max-width` queries).
- ❌ `100vh` on mobile.
- ❌ Fixed-width elements causing horizontal scroll.
- ❌ Tiny tap targets.
- ❌ Hover-only menus.
- ❌ Tiny font sizes on mobile (< 16px — triggers iOS zoom).
- ❌ Forgetting to test real devices.

## Testing

- Chrome DevTools device emulation (good for layout, not perf).
- BrowserStack / LambdaTest (real devices).
- Your actual phone (always).
- Resize the browser window and watch for breaks.
- Lighthouse mobile.

## References

- MDN Responsive Design: https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Responsive_Design
- web.dev Responsive: https://web.dev/learn/design
- Tailwind responsive: https://tailwindcss.com/docs/responsive-design

## Further Reading

- *Responsive Web Design* — Ethan Marcotte (the original A List Apart article)

## Exercises

1. Take a desktop-only site. Make it fully responsive.
2. Build a layout that uses container queries.
3. Build a nav that's a drawer on mobile, horizontal on desktop.

## Projects

- Build a responsive dashboard (mobile: stacked, desktop: sidebar + grid).
- Build a responsive pricing page.

---

**Previous:** [Accessibility/](../Accessibility/) · **Next:** [Flexbox/](../Flexbox/) · **Related:** [Grid/](../Grid/), [Performance/](../Performance/)
