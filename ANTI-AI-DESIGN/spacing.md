# Anti-AI-Design: Spacing

> Vary spacing intentionally. Don't `py-24` every section.

---

## The AI tell

Every section has the same padding (`py-24`), the same gap (`gap-6`), the same margins. Looks mechanical.

---

## Human approach

### 1. Spacing scale
Use a scale (4 / 8 / 12 / 16 / 24 / 32 / 48 / 64 / 96 / 128). Don't use magic numbers.

### 2. Vary section padding
- Hero: large (`py-32` or `py-40`).
- Feature sections: medium (`py-20` or `py-24`).
- Footer: smaller (`py-12` or `py-16`).
- Inline content sections: tighter (`py-12`).

### 3. Vary gap within sections
- Cards in a grid: `gap-6`.
- Dense list: `gap-2` or `gap-3`.
- Hero text + CTA: `gap-4`.
- Section title + content: `gap-12`.

### 4. Asymmetric spacing
- Hero: more space above title than below.
- Cards: tighter top, more bottom (for "lift").
- Off-center alignment creates visual interest.

### 5. Breathing room for important elements
- Hero: lots of space.
- Critical CTA: lots of space.
- Dense data table: tight spacing.

### 6. Mobile
- Don't crush mobile. Maintain proportions.
- Use `clamp()` for fluid spacing.

---

## Patterns

### Pattern: Hero with breathing room
```css
.hero {
  padding-top: 6rem;     /* big top */
  padding-bottom: 4rem;  /* less bottom */
}
.hero h1 { margin-bottom: 1.5rem; }
.hero .cta { margin-top: 2rem; }
```

### Pattern: Feature grid
```css
.features {
  padding-top: 4rem;
  padding-bottom: 4rem;
}
.features .grid { gap: 2rem; }
.features h2 { margin-bottom: 3rem; }
```

### Pattern: Dense footer
```css
.footer {
  padding-top: 3rem;
  padding-bottom: 3rem;
}
.footer .grid { gap: 1rem; }
```

### Pattern: Fluid spacing
```css
.section {
  padding-top: clamp(3rem, 8vw, 6rem);
  padding-bottom: clamp(3rem, 8vw, 6rem);
}
```

---

## Common mistakes

- ❌ Every section `py-24`.
- ❌ Every gap `gap-6`.
- ❌ Same margin top and bottom everywhere.
- ❌ Magic numbers (`margin-top: 47px`).
- ❌ Crushing mobile (no fluid scaling).

---

## The rule

**Don't use the same spacing value twice in a row.** If hero is `py-32`, next section should be `py-20` or `py-24`, not `py-32`.

Variation creates rhythm. Rhythm creates humanity.

---

**Next:** [layouts.md](layouts.md) · Back to [ANTI-AI-DESIGN/](README.md)
