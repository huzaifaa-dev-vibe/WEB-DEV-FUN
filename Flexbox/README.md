# Flexbox

> 1D layout system. Use for rows OR columns.

---

## Purpose

Master Flexbox for navbars, button groups, card rows, alignment, and anywhere you need 1D layout.

## Prerequisites

- [CSS/](../CSS/) basics.

## Learning Outcome

You can build any 1D layout without floats, inline-block hacks, or absolute positioning.

## Dependencies

- CSS.

## Related Files

- [CSS/](../CSS/) · [Grid/](../Grid/) · [Responsive-Design/](../Responsive-Design/) · [Flexbox/cheat-sheet.md](cheat-sheet.md) · [Flexbox/examples.md](examples.md)

## AI Instructions

When laying out elements in 1D:
1. Use Flexbox (`display: flex`).
2. Use `gap` for spacing. Not margin.
3. `flex-direction: column` for vertical.
4. `align-items` for cross-axis. `justify-content` for main-axis.
5. `flex: 1` to fill space, `flex-shrink: 0` to prevent.
6. `min-width: 0` if a flex child won't shrink.
7. `flex-wrap: wrap` for responsive wrapping.

## Human Notes

### Flex container properties
- `display: flex` — enable.
- `flex-direction: row | row-reverse | column | column-reverse`
- `flex-wrap: nowrap | wrap | wrap-reverse`
- `flex-flow: <direction> <wrap>` — shorthand.
- `justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly` — main axis.
- `align-items: stretch | flex-start | flex-end | center | baseline` — cross axis.
- `align-content: ...` — multi-line (rare).
- `gap: <length>` — spacing between items.

### Flex item properties
- `flex-grow: <number>` — grow factor.
- `flex-shrink: <number>` — shrink factor.
- `flex-basis: <length> | auto` — base size.
- `flex: <grow> <shrink> <basis>` — shorthand. `flex: 1` = `1 1 0`.
- `order: <number>` — reorder (default 0).
- `align-self: ...` — override align-items for one item.

### Common patterns

```css
/* Center anything */
.center { display: flex; align-items: center; justify-content: center; }

/* Space between (navbar) */
.nav { display: flex; justify-content: space-between; align-items: center; }

/* Sticky footer */
.layout { display: flex; flex-direction: column; min-height: 100dvh; }
.layout main { flex: 1; }

/* Card row that wraps */
.cards { display: flex; flex-wrap: wrap; gap: 1rem; }
.cards > * { flex: 1 1 250px; }

/* Sidebar + content */
.app { display: flex; gap: 1rem; }
.sidebar { flex: 0 0 250px; }
.content { flex: 1; min-width: 0; }
```

### The `min-width: 0` gotcha
Flex items default to `min-content` minimum width. Long content (URLs, code) won't shrink.

Fix: `min-width: 0` on the flex child.

### Gap support
All modern browsers support `gap` in Flexbox. Use it instead of margins.

## Common Mistakes

- ❌ Using `margin: auto` for centering (use `justify-content`/`align-items`).
- ❌ Forgetting `min-width: 0` on flex children with long content.
- ❌ `flex: 1` when you mean `flex: 1 0 auto`.
- ❌ Using Flexbox for 2D layouts (use Grid).

## Tools

- Flexbox Froggy (game): https://flexboxfroggy.com/
- Flexbox Defense (game): https://www.flexboxdefense.com/

## References

- MDN Flexbox: https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox
- CSS-Tricks Complete Guide: https://css-tricks.com/snippets/css/a-guide-to-flexbox/
- web.dev: https://web.dev/learn/css/flexbox

## Exercises

1. Build a navbar with logo left, links right, mobile hamburger.
2. Build a sticky footer layout.
3. Build a card grid that wraps responsively.

## Projects

- Build a media object (image + text) layout.
- Build a toolbar with grouped buttons.

---

**Previous:** [Responsive-Design/](../Responsive-Design/) · **Next:** [Grid/](../Grid/) · **Related:** [CSS/](../CSS/)
