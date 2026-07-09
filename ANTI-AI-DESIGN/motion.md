# Anti-AI-Design: Motion

> Motion explains state. Not decoration.

---

## The AI tells

1. `fade-in-up` on every section.
2. Auto-rotating carousels.
3. Parallax on hero (for its own sake).
4. Floating animations on cards.
5. Long durations (1s+) for simple state changes.
6. Auto-playing video that can't be paused.
7. No `prefers-reduced-motion` fallback.
8. Animations on layout properties (`width`, `top`, `left`).

---

## Human approach

### 1. Motion has purpose
- **State change** — modal opens, list reorders, item added.
- **Spatial continuity** — element moves from A to B.
- **Feedback** — button press, toggle on/off.
- **Progress** — loading, upload progress.

If motion doesn't do one of these, remove it.

### 2. Short durations
- 100-200ms for micro-interactions.
- 200-300ms for state changes.
- 300-500ms for page transitions.
- 500-800ms for hero entrances (one per page max).

### 3. Proper easing
- `ease-out` for entrances.
- `ease-in` for exits.
- `cubic-bezier(0.16, 1, 0.3, 1)` for smooth decel.
- NOT `linear` (except for spinners).

### 4. Only `transform` and `opacity`
- Animate `transform` (translate, scale, rotate).
- Animate `opacity`.
- Never `width`, `height`, `top`, `left`, `margin` (causes layout, jank).

### 5. Respect reduced motion
```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

### 6. Stagger (sparingly)
- For lists, stagger entrance by 30-50ms per item.
- Don't stagger more than 5-7 items.

### 7. Exit animations
- Modal close should animate out (not just disappear).
- Use `AnimatePresence` (Framer Motion).

---

## Patterns

### Pattern: Page enter
```jsx
<motion.main
  initial={{ opacity: 0, y: 8 }}
  animate={{ opacity: 1, y: 0 }}
  transition={{ duration: 0.3, ease: [0.16, 1, 0.3, 1] }}
>
```

### Pattern: Modal
```jsx
<AnimatePresence>
  {open && (
    <motion.div
      initial={{ opacity: 0, scale: 0.95 }}
      animate={{ opacity: 1, scale: 1 }}
      exit={{ opacity: 0, scale: 0.95 }}
      transition={{ duration: 0.2 }}
    >
```

### Pattern: List reorder
```jsx
<motion.div layout>
  {items.map(item => <motion.div layout key={item.id} />)}
</motion.div>
```

### Pattern: Button press
```css
.button:active { transform: scale(0.97); transition: transform 100ms; }
```

### Pattern: Hover lift
```css
.card:hover { transform: translateY(-2px); transition: transform 150ms; }
```

---

## When NOT to animate

- Every section fade-in. (Just show the content.)
- Every hover. (Some hovers should be instant — like link color change.)
- Carousels. (Just show static content.)
- Parallax. (Almost never worth the perf cost.)

---

## Common mistakes

- ❌ Auto-rotating testimonials carousel.
- ❌ Fade-in-up on every section.
- ❌ Long durations.
- ❌ Linear easing.
- ❌ Animating layout properties.
- ❌ No reduced-motion fallback.
- ❌ Motion that delays content (like 1s entrance for hero text).

---

## Tools

- Framer Motion: https://www.framer.com/motion/
- GSAP: https://gsap.com/
- Motion One: https://motion.dev/
- Web Animations API (native).

---

**Next:** [testimonials.md](testimonials.md) · Back to [ANTI-AI-DESIGN/](README.md)
