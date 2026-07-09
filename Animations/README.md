# Animations

> Motion should explain, not decorate. Respect users who don't want it.

---

## Purpose

Master CSS, JS, and Web Animations API for performant, accessible motion.

## Prerequisites

- [CSS/](../CSS/), [JavaScript/](../JavaScript/).

## Learning Outcome

You can build delightful, accessible animations that don't kill performance.

## Dependencies

- CSS / JS.

## Related Files

- [Animations/css.md](css.md) · [Animations/framer-motion.md](framer-motion.md) · [Animations/performance.md](performance.md) · [Animations/accessibility.md](accessibility.md) · [ANTI-AI-DESIGN/motion.md](../ANTI-AI-DESIGN/motion.md)

## AI Instructions

When animating:
1. **Animate only `transform` and `opacity`.** Never `width`/`height`/`top`/`left`/`margin` (causes layout).
2. **Respect `prefers-reduced-motion`.** Always.
3. **Duration: 150–300ms** for UI feedback, 400–600ms for entrances.
4. **Easing: cubic-bezier** over linear.
5. **Purpose:** animation explains a state change. No purpose? Don't animate.
6. **Don't over-animate.** One hero animation, not 30 fade-ins.

## Human Notes

### Performance rules
- Only `transform` and `opacity` are GPU-accelerated and don't trigger layout.
- For other properties, the browser repaints. Slow.
- `will-change` — hint to browser, but use sparingly.
- Use `transform: translateZ(0)` to force a layer (also sparingly).

### Reduced motion
```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

### Durations (general guidance)
- Micro-interactions: 100–200ms.
- Hover/active states: 150ms.
- Modal opens: 200–300ms.
- Page transitions: 300–500ms.
- Hero entrance: 500–800ms.
- Loading spinners: 1s+ (loop).

### Easings
- `ease-out` — start fast, end slow. Good for entrances.
- `ease-in` — start slow, end fast. Good for exits (rare).
- `ease-in-out` — both. Good for state changes.
- `linear` — for progress bars/spinners only.
- Custom: `cubic-bezier(0.34, 1.56, 0.64, 1)` (overshoot), `cubic-bezier(0.16, 1, 0.3, 1)` (smooth decel).

## CSS Animations

### Transition (state change)
```css
.button {
  background: blue;
  transition: background 150ms ease-out;
}
.button:hover { background: darkblue; }
.button:active { transform: scale(0.97); }
```

### Keyframe animation (autonomous)
```css
@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(8px); }
  to { opacity: 1; transform: translateY(0); }
}
.fade-in {
  animation: fadeInUp 300ms cubic-bezier(0.16, 1, 0.3, 1);
}
```

### Stagger
```css
.item {
  opacity: 0;
  animation: fadeInUp 300ms ease-out forwards;
}
.item:nth-child(1) { animation-delay: 0ms; }
.item:nth-child(2) { animation-delay: 50ms; }
.item:nth-child(3) { animation-delay: 100ms; }
```

## Framer Motion (Motion)

Best React animation library.

```jsx
import { motion, AnimatePresence } from 'framer-motion';

function Modal({ open, onClose }) {
  return (
    <AnimatePresence>
      {open && (
        <motion.div
          initial={{ opacity: 0, scale: 0.95 }}
          animate={{ opacity: 1, scale: 1 }}
          exit={{ opacity: 0, scale: 0.95 }}
          transition={{ duration: 0.2, ease: [0.16, 1, 0.3, 1] }}
        >
          Modal content
        </motion.div>
      )}
    </AnimatePresence>
  );
}
```

→ [Animations/framer-motion.md](framer-motion.md) for deep dive.

## Web Animations API

```js
element.animate(
  [
    { opacity: 0, transform: 'translateY(8px)' },
    { opacity: 1, transform: 'translateY(0)' },
  ],
  { duration: 300, easing: 'ease-out', fill: 'forwards' }
);
```

Native, performant, JS-controlled.

## View Transitions API (page transitions)

```js
// Same-document navigation
document.startViewTransition(() => {
  // Update DOM
});

// Cross-document (MPA) — opt-in via meta
// <meta name="view-transition" content="same-origin">
```

→ [Animations/view-transitions.md](view-transitions.md)

## Scroll-driven animations

```css
@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}
.hero {
  animation: fadeIn linear;
  animation-timeline: view();
  animation-range: entry 0% cover 30%;
}
```

Pure CSS, scroll-based progress.

## Common Patterns

### Hover lift
```css
.card { transition: transform 200ms ease-out, box-shadow 200ms ease-out; }
.card:hover { transform: translateY(-4px); box-shadow: 0 10px 30px rgba(0,0,0,0.1); }
```

### Button press
```css
.button:active { transform: scale(0.97); }
```

### Loading spinner
```css
.spinner { animation: spin 1s linear infinite; }
@keyframes spin { to { transform: rotate(360deg); } }
```

### Skeleton shimmer
```css
.skeleton {
  background: linear-gradient(90deg, #eee 25%, #f5f5f5 50%, #eee 75%);
  background-size: 200% 100%;
  animation: shimmer 1.5s infinite;
}
@keyframes shimmer {
  to { background-position: -200% 0; }
}
```

### Page enter
```css
@keyframes pageEnter {
  from { opacity: 0; transform: translateY(8px); }
  to { opacity: 1; transform: translateY(0); }
}
main { animation: pageEnter 300ms ease-out; }
```

## Common Mistakes

- ❌ Animating layout properties (`width`, `top`, `left`).
- ❌ No reduced-motion fallback.
- ❌ Animating everything (paralysis).
- ❌ Too long / too slow.
- ❌ Linear easing for organic motion.
- ❌ Auto-playing motion that triggers vestibular issues.

## Tools

- Framer Motion docs: https://www.framer.com/motion/
- GSAP: https://gsap.com/
- Lottie: https://lottiefiles.com/
- Rive: https://rive.app/
- Theatre.js: https://www.theatrejs.com/

## References

- CSS-Tricks Animation: https://css-tricks.com/almanac/properties/a/animation/
- web.dev Animations: https://web.dev/articles/animations-guide
- Easings cheat sheet: https://easings.net/

## Exercises

1. Build a button with hover lift + active press.
2. Build a modal with fade + scale.
3. Build a list with staggered entrance.
4. Build a scroll-triggered animation.
5. Implement reduced-motion fallback.

## Projects

- Build an animated landing page with scroll-driven animations.
- Build a sortable list with smooth item reordering (Framer Motion `layout`).

---

**Previous:** [Grid/](../Grid/) · **Next:** [Design-Patterns/](../Design-Patterns/) · **Related:** [ANTI-AI-DESIGN/](../ANTI-AI-DESIGN/), [Performance/](../Performance/)
