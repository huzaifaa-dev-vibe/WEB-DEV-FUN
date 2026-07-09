# Modern Gradients

> Use gradients intentionally. Not as AI-tell.

---

## The rule

Gradients should:
- Be subtle (not rainbow).
- Use 2 colors (not 5).
- NOT be the default purple-to-pink.
- Have a purpose (depth, focal point, brand expression).

---

## Acceptable gradients

### Subtle brand (depth)
```css
background: linear-gradient(135deg, #4f46e5 0%, #6366f1 100%);
/* subtle indigo shift, not rainbow */
```

### Mesh background (rare, intentional)
```css
background:
  radial-gradient(circle at 20% 20%, #4f46e5 0%, transparent 50%),
  radial-gradient(circle at 80% 80%, #06b6d4 0%, transparent 50%),
  #0a0a0a;
```

### Text accent (use sparingly)
```css
background: linear-gradient(135deg, #f97316, #ec4899);
-webkit-background-clip: text;
background-clip: text;
color: transparent;
```
Don't use for body text. Only headlines, only one word.

### Image overlay (legibility)
```css
background: linear-gradient(to top, rgba(0,0,0,0.7), transparent);
```

### Glass effect (rare)
```css
background: rgba(255, 255, 255, 0.05);
backdrop-filter: blur(12px);
```
Use sparingly. The "glassmorphism on purple gradient" is a major AI tell.

---

## Forbidden gradients

- ❌ Purple to pink (`from-purple-500 to-pink-500`).
- ❌ Rainbow (5+ colors).
- ❌ Blue to purple (overused).
- ❌ Sunset gradient on every hero.
- ❌ Gradient on body text.
- ❌ Gradient backgrounds under text without overlay.

---

## Examples

### Logo / mark
```css
.logo-mark {
  background: linear-gradient(135deg, #f97316, #ec4899);
  /* orange to pink, intentional */
}
```

### Hero overlay (image)
```css
.hero-image {
  background:
    linear-gradient(to top, rgba(0,0,0,0.85), transparent 60%),
    url('/hero.jpg');
}
```

### Accent button (subtle)
```css
.button-primary {
  background: linear-gradient(180deg, #4f46e5, #4338ca);
  /* dark indigo shift, gives depth */
}
```

### Background blob (decorative)
```css
.blob {
  position: absolute;
  width: 600px; height: 600px;
  background: radial-gradient(circle, rgba(79, 70, 229, 0.3), transparent 70%);
  filter: blur(80px);
}
```

---

## When NOT to use gradients

- Body text.
- Card backgrounds (use solid color).
- Section backgrounds (use solid + maybe a subtle blob).
- Every button (one accent color is fine).
- As a default — only when intentional.

---

## Test

If your gradient could be replaced with a solid color and the design would look just as good — use the solid color.

---

**Back to:** [Color-Palettes/](README.md) · [ANTI-AI-DESIGN/color.md](../ANTI-AI-DESIGN/color.md)
