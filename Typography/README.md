# Typography

> Type is the voice of your design. Get it wrong and nothing else matters.

---

## Purpose

Master font selection, pairing, scale, hierarchy, and performance.

## Prerequisites

- [CSS/](../CSS/).

## Learning Outcome

You can pick fonts that fit a brand, pair them well, build a type scale, and ship them performantly.

## Dependencies

- CSS.

## Related Files

- [CSS/](../CSS/) · [Color-Palettes/](../Color-Palettes/) · [ANTI-AI-DESIGN/](../ANTI-AI-DESIGN/) · [Typography/scale.md](scale.md) · [Typography/pairing.md](pairing.md) · [Typography/performance.md](performance.md)

## AI Instructions

When choosing type:
1. **Pick ONE typeface family** with multiple weights. Add a second for display only if needed.
2. **Build a type scale** (12 / 14 / 16 / 18 / 20 / 24 / 30 / 36 / 48 / 60).
3. **Use `rem`** for sizes (not `px`).
4. **Line-height**: 1.5–1.6 for body, 1.1–1.3 for headings.
5. **Letter-spacing**: tight for big headings, normal for body.
6. **Max measure** (line length): 60–80 chars.
7. **Self-host fonts** (Fontsource) or use a privacy-friendly CDN (Bunny Fonts).
8. **`font-display: swap`**, `preload` critical font.
9. **Subset** to languages you use.
10. **Variable fonts** when possible (one file, many weights).

## Human Notes

### Type categories
- **Serif** — traditional, editorial, trustworthy. (e.g., Source Serif, Lora.)
- **Sans-serif** — modern, clean, default for UI. (e.g., Inter, Geist, SF Pro.)
- **Mono** — code, technical. (e.g., JetBrains Mono, Fira Code.)
- **Display** — decorative, headlines only.
- **Script** — accents only, never body.

### Type scale (modular)
Use a ratio (1.2, 1.25, 1.333, 1.5).
- Base: 16px (1rem).
- 1.25 ratio: 16 / 20 / 25 / 31 / 39 / 49 / 61 / 76.

```css
:root {
  --text-xs: 0.75rem;   /* 12 */
  --text-sm: 0.875rem;  /* 14 */
  --text-base: 1rem;    /* 16 */
  --text-lg: 1.125rem;  /* 18 */
  --text-xl: 1.25rem;   /* 20 */
  --text-2xl: 1.5rem;   /* 24 */
  --text-3xl: 1.875rem; /* 30 */
  --text-4xl: 2.25rem;  /* 36 */
  --text-5xl: 3rem;     /* 48 */
  --text-6xl: 3.75rem;  /* 60 */
}
```

### Line height
- Body: 1.5–1.6.
- Headings: 1.1–1.3.
- UI: 1.4–1.5.

### Letter spacing
- Body: normal (0).
- Headings (large): -0.02em to -0.04em.
- Caps / labels: 0.05em to 0.1em.

### Measure (line length)
- 60–80 chars for body.
- Use `max-width: 65ch`.

### Font weight
- Body: 400 (regular).
- Medium / strong: 500.
- Headings: 600–700.
- Display: 700+.

### Modern UI fonts (defaults that won't steer you wrong)
- **Inter** — most popular UI sans. Works for everything.
- **Geist** — Vercel's font. Modern, geometric.
- **SF Pro / SF UI** — Apple's font (only on Apple devices; bundle Inter as fallback).
- **Roboto** — Android default. Works on web too.
- **IBM Plex Sans** — humanist, slightly editorial.
- **Manrope** — geometric, friendly.
- **Outfit** — modern geometric.
- **Space Grotesk** — distinctive, good for tech.
- **DM Sans** — clean, friendly.
- **Plus Jakarta Sans** — modern, geometric.

### Editorial / Serif fonts
- **Source Serif** — Adobe's. Solid.
- **Lora** — slightly calligraphic.
- **Crimson Pro** — book-like.
- **EB Garamond** — classic.
- **Newsreader** — modern editorial.
- **Fraunces** — display serif with personality.

### Mono fonts
- **JetBrains Mono** — ligatures.
- **Fira Code** — ligatures.
- **IBM Plex Mono** — humanist.
- **Geist Mono** — Vercel's.
- **Space Mono** — distinctive.

### Pairings (safe)
- Inter + Inter (single family, weight contrast).
- Inter + Source Serif (sans body, serif headings).
- Geist + Geist Mono (sans + code).
- Manrope + Fraunces (modern + editorial).
- Space Grotesk + Inter (display + body).

→ [Typography/pairing.md](pairing.md) for more.

### Performance
- Self-host with Fontsource: https://fontsource.org/
- Or use Bunny Fonts (privacy-friendly Google Fonts mirror): https://fonts.bunny.net/
- `font-display: swap` — show fallback immediately.
- `preload` critical font.
- Subset to Latin if you only need Latin.
- Variable fonts = one file, all weights.

→ [Typography/performance.md](performance.md)

```html
<link rel="preconnect" href="https://fonts.bunny.net">
<link rel="preload" as="font" href="/fonts/inter-var.woff2" type="font/woff2" crossorigin>
```

```css
@font-face {
  font-family: 'Inter';
  src: url('/fonts/inter-var.woff2') format('woff2-variations');
  font-weight: 100 900;
  font-display: swap;
  font-style: normal;
}

body {
  font-family: 'Inter', system-ui, sans-serif;
  font-feature-settings: 'cv02', 'cv03', 'cv04', 'cv11';
}
```

### Fallback fonts
Always declare fallbacks:
```css
font-family: 'Inter', system-ui, -apple-system, sans-serif;
font-family: 'JetBrains Mono', 'SF Mono', Menlo, monospace;
```

This prevents "Times New Roman" disasters.

### Variable fonts
One file, infinite weights. Modern, performant.
```css
font-variation-settings: 'wght' 450, 'wdth' 100;
```

### OpenType features
```css
font-feature-settings: 'liga' 1, 'kern' 1, 'calt' 1, 'ss01' 1;
```
- `liga` — ligatures (fi, fl).
- `kern` — kerning.
- `calt` — contextual alternates.
- `ss01`–`ss20` — stylistic sets (font-specific).
- `tnum` — tabular numbers (for tables/data).

## Common Mistakes

- ❌ Too many fonts (limit to 2).
- ❌ No fallbacks.
- ❌ `px` for font size (use `rem`).
- ❌ Long line lengths (no `max-width`).
- ❌ Tight line height on body.
- ❌ Loose letter spacing on body.
- ❌ Light weights for body text (poor contrast).
- ❌ Google Fonts blocking render.
- ❌ Loading every weight when you use 2.

## Tools

- Fontsource: https://fontsource.org/
- Google Fonts: https://fonts.google.com/
- Bunny Fonts: https://fonts.bunny.net/
- Font Pair: https://www.fontpair.co/
- Typewolf: https://www.typewolf.com/
- Fonts In Use: https://fontsinuse.com/
- Variable Fonts: https://v-fonts.com/
- Type Scale: https://typescale.com/

## References

- Practical Typography: https://practicaltypography.com/
- web.dev Fonts: https://web.dev/articles/font-best-practices
- MDN text styling: https://developer.mozilla.org/en-US/docs/Learn/CSS/Styling_text

## Further Reading

- *Practical Typography* — Matthew Butterick (free)
- *The Elements of Typographic Style* — Robert Bringhurst
- *Thinking with Type* — Ellen Lupton
- *On Web Typography* — Jason Santa Maria

## Exercises

1. Build a type scale using `rem` and CSS variables.
2. Pair two fonts and use them on a landing page.
3. Self-host a variable font. Set up `font-display: swap` and `preload`.
4. Set up tabular numbers for a data table.

## Projects

- Design a typography system for a SaaS dashboard.
- Build a blog with editorial-quality typography.

---

**Previous:** [UX/](../UX/) · **Next:** [Icons/](../Icons/) · **Related:** [CSS/](../CSS/), [ANTI-AI-DESIGN/](../ANTI-AI-DESIGN/)
