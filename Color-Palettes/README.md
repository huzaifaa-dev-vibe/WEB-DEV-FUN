# Color Palettes

> Curated palettes by use case. Pick one. Stay.

---

## Purpose

Provide ready-to-use color palettes for common web app types. Pick one, copy the tokens, ship.

## Prerequisites

- [CSS/](../CSS/), [ANTI-AI-DESIGN/color.md](../ANTI-AI-DESIGN/color.md).

## Learning Outcome

You can pick a palette that fits your brand and use it consistently.

## Dependencies

- CSS.

## Related Files

- [ANTI-AI-DESIGN/color.md](../ANTI-AI-DESIGN/color.md) · [CSS/variables.md](../CSS/variables.md) · [Color-Palettes/professional.md](professional.md) · [Color-Palettes/startup.md](startup.md) · [Color-Palettes/dark.md](dark.md) · [Color-Palettes/gradients.md](gradients.md)

## AI Instructions

When picking a palette:
1. **Pick ONE palette** for the project. Don't mix.
2. **Limit to 5 colors** (bg, fg, muted, accent, surface).
3. **Use OKLCH**.
4. **Test contrast** (4.5:1 body, 3:1 large).
5. **Dark mode** included.
6. **Not purple-to-pink gradient.**

## Human Notes

→ See individual files for full palettes:
- [professional.md](professional.md)
- [startup.md](startup.md)
- [minimal.md](minimal.md)
- [dark.md](dark.md)
- [luxury.md](luxury.md)
- [healthcare.md](healthcare.md)
- [fintech.md](fintech.md)
- [education.md](education.md)
- [gaming.md](gaming.md)
- [ai.md](ai.md)
- [portfolio.md](portfolio.md)
- [corporate.md](corporate.md)
- [gradients.md](gradients.md)

## How to use a palette

```css
:root {
  /* from palette */
  --color-bg: #fafaf9;
  --color-fg: #1c1917;
  --color-muted: #78716c;
  --color-accent: #9f1239;
  --color-surface: #ffffff;
  --color-border: #e7e5e4;
}

.dark {
  /* dark mode variant */
  --color-bg: #0a0a0a;
  --color-fg: #fafafa;
  --color-muted: #a8a29e;
  --color-surface: #171717;
  --color-border: #262626;
}
```

Then use everywhere:
```css
body { background: var(--color-bg); color: var(--color-fg); }
.button { background: var(--color-accent); color: white; }
.card { background: var(--color-surface); border: 1px solid var(--color-border); }
```

## Color spaces

- **OKLCH** (recommended) — perceptually uniform.
- **HSL** — common but not perceptually uniform.
- **HEX** — universal but opaque.
- **RGB** — low-level.

Use OKLCH for new projects.

```css
:root {
  --color-accent: oklch(60% 0.2 250);
}
```

## Tools

- OKLCH picker: https://oklch.com/
- Coolors: https://coolors.co/
- Realtime Colors: https://www.realtimecolors.com/
- Happy Hues: https://www.happyhues.co/
- ColorBox: https://colorbox.io/
- Huetone: https://huetone.ardov.me/
- WebAIM contrast: https://webaim.org/resources/contrastchecker/

## References

- Refactoring UI (color chapter): https://www.refactoringui.com/
- Practical Color: https://refactoringui.com/books/practical-color/

## Exercises

1. Pick a palette. Apply to your project.
2. Generate dark mode variant.
3. Test contrast for every text/bg combination.

## Projects

- Build a brand palette generator tool.

---

**Previous:** [ANTI-AI-DESIGN/](../ANTI-AI-DESIGN/) · **Next:** [Projects/](../Projects/) · **Related:** [CSS/](../CSS/)
