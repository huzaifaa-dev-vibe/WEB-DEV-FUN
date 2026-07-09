# Anti-AI-Design: Typography

> Type that has voice. Not the AI default.

---

## The AI tells

1. `text-3xl font-bold` for every heading.
2. `Inter` font everywhere (without customization).
3. Long line lengths (no `max-width`).
4. Tight line heights (1.2 for body).
5. No type scale (magic sizes).
6. `<br>` for spacing.
7. Multiple display fonts (4+).

---

## Human approach

### 1. Pick one typeface
- Inter (default), Geist, IBM Plex Sans, Manrope, etc.
- Or pair sans + serif for editorial.

→ [Typography/](../Typography/) for font picks.

### 2. Build a type scale
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
  --text-7xl: 4.5rem;   /* 72 */
}
```

### 3. Fluid type
```css
h1 { font-size: clamp(2.5rem, 6vw, 5rem); }
```

### 4. Line height
- Body: 1.5–1.6.
- Headings: 1.1–1.3.
- UI: 1.4.

### 5. Letter spacing
- Body: normal.
- Large headings: -0.02em to -0.04em.
- Caps / labels: 0.05em to 0.1em.

### 6. Max measure
- 60-80 chars for body.
- `max-width: 65ch`.

### 7. Weight contrast
- Body: 400.
- Strong: 500.
- Headings: 600-700.
- Display: 700-900.

Don't use 400 for everything. Don't use 700 for everything.

### 8. Variable fonts
- One file, infinite weights.
- `font-variation-settings: 'wght' 450`.

### 9. Self-host
- Fontsource: https://fontsource.org/.
- Or Bunny Fonts (privacy): https://fonts.bunny.net/.

### 10. `font-display: swap`
- Prevents invisible text.
- `preload` critical font.

---

## Patterns

### Pattern: Big editorial headline
```css
.hero h1 {
  font-size: clamp(3rem, 8vw, 7rem);
  line-height: 0.95;
  letter-spacing: -0.04em;
  font-weight: 700;
}
```

### Pattern: Mixed weights
```html
<h1>
  <span class="font-light">Ship</span>
  <span class="font-bold">faster</span>
  <span class="font-light italic">than ever</span>
</h1>
```

### Pattern: Mono accent
```html
<p>
  <span class="font-mono text-sm text-muted">v1.0.0</span>
  Released yesterday.
</p>
```

### Pattern: Numbered sections
```html
<div class="flex gap-4">
  <span class="font-mono text-sm text-muted">01</span>
  <h2>How it works</h2>
</div>
```

### Pattern: Italic for emphasis (not bold)
```html
<p>This is <em>really</em> important.</p>
```

---

## What to avoid

- ❌ `text-3xl font-bold` everywhere.
- ❌ Multiple display fonts.
- ❌ No `max-width` (long lines).
- ❌ `<br>` for spacing.
- ❌ Centered long paragraphs.
- ❌ Tight line height on body.
- ❌ No fluid scaling (fixed `px`).

---

**Next:** [radii.md](radii.md) · Back to [ANTI-AI-DESIGN/](README.md)
