# Grid

> 2D layout system. Use for pages, dashboards, complex card layouts.

---

## Purpose

Master CSS Grid for 2D layouts — pages, dashboards, complex card grids, and anywhere you need rows AND columns.

## Prerequisites

- [CSS/](../CSS/), [Flexbox/](../Flexbox/).

## Learning Outcome

You can build any 2D layout with confidence.

## Dependencies

- CSS.

## Related Files

- [CSS/](../CSS/) · [Flexbox/](../Flexbox/) · [Responsive-Design/](../Responsive-Design/) · [Grid/cheat-sheet.md](cheat-sheet.md) · [Grid/examples.md](examples.md)

## AI Instructions

When laying out 2D:
1. Use Grid (`display: grid`).
2. Use `gap` for spacing.
3. `grid-template-columns: repeat(auto-fit, minmax(250px, 1fr))` for responsive card grids.
4. Use `grid-template-areas` for page layouts.
5. `subgrid` for aligning children to parent grid.
6. Use Grid for the page, Flexbox for components inside.

## Human Notes

### Grid container properties
- `display: grid`
- `grid-template-columns: <track-size>...` — e.g., `1fr 2fr 1fr`, `repeat(3, 1fr)`, `repeat(auto-fit, minmax(250px, 1fr))`.
- `grid-template-rows: <track-size>...`
- `grid-template-areas: "header header" "sidebar main" "footer footer"`
- `gap: <row> <col>` (or `row-gap` / `column-gap`)
- `justify-items: start | end | center | stretch`
- `align-items: start | end | center | stretch`
- `justify-content: ...` (whole grid in container)
- `align-content: ...`

### Grid item properties
- `grid-column: <start> / <end>` or `span <n>` — e.g., `1 / 3` or `span 2`.
- `grid-row: <start> / <end>`
- `grid-area: <name>` (if using template-areas)
- `justify-self: ...` / `align-self: ...`

### Track sizes
- `1fr` — fraction of remaining space.
- `minmax(min, max)` — bounded.
- `auto` — content-sized.
- `fit-content(<max>)` — content-sized with cap.
- `subgrid` — inherit parent's tracks.

### Common patterns

```css
/* Responsive card grid (no media queries needed!) */
.cards {
  display: grid;
  gap: 1rem;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
}

/* Page layout with areas */
.page {
  display: grid;
  grid-template-areas:
    "header header"
    "sidebar main"
    "footer footer";
  grid-template-columns: 250px 1fr;
  grid-template-rows: auto 1fr auto;
  min-height: 100dvh;
}
.header { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main { grid-area: main; }
.footer { grid-area: footer; }

/* Sidebar collapses on mobile */
@media (max-width: 768px) {
  .page {
    grid-template-areas:
      "header"
      "main"
      "footer";
    grid-template-columns: 1fr;
  }
  .sidebar { display: none; }
}

/* Holy grail layout */
.holy-grail {
  display: grid;
  grid-template:
    "header header header" auto
    "left   main   right" 1fr
    "footer footer footer" auto
    / 200px 1fr 200px;
  min-height: 100dvh;
}

/* Center anything */
.center {
  display: grid;
  place-items: center;
}
```

### Auto-fit vs auto-fill
- `auto-fit` — empty tracks collapse. Items stretch to fill.
- `auto-fill` — empty tracks stay. Items don't stretch.

Use `auto-fit` for "fill the row" card grids.

### Subgrid (now widely supported)
```css
.parent {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr;
}
.child {
  display: grid;
  grid-template-columns: subgrid; /* inherits parent's columns */
  grid-column: span 3;
}
```

Great for aligning card titles/descriptions across a row.

## Common Mistakes

- ❌ Using Grid for 1D layouts (use Flexbox).
- ❌ Hard-coded grid columns when `auto-fit` + `minmax` would respond.
- ❌ Not using `gap`.
- ❌ `1fr 1fr 1fr` instead of `repeat(3, 1fr)`.

## Tools

- Grid Garden (game): https://cssgridgarden.com/
- Grid Layoutit: https://grid.layoutit.com/

## References

- MDN Grid: https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_grid_layout
- CSS-Tricks Complete Guide: https://css-tricks.com/snippets/css/complete-guide-grid/
- web.dev: https://web.dev/learn/css/grid

## Exercises

1. Build a dashboard layout (header, sidebar, main, footer).
2. Build a card grid that auto-fits 1-4 columns.
3. Build the "holy grail" layout.

## Projects

- Build a photo gallery with mixed-size cells.
- Build a responsive kanban board.

---

**Previous:** [Flexbox/](../Flexbox/) · **Next:** [Animations/](../Animations/) · **Related:** [CSS/](../CSS/)
