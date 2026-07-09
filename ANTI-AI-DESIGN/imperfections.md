# Anti-AI-Design: Imperfections

> Perfect = AI. Imperfect = human.

---

## Why imperfection matters

AI defaults to symmetry, alignment, consistency. Everything is perfectly balanced. That's the tell.

Human design has small imperfections:
- Slight rotation.
- Hand-drawn elements.
- Asymmetric details.
- Off-grid elements.
- Mixed weights / sizes.

These signal: a person made this.

---

## Types of intentional imperfection

### 1. Slight rotation
- Hero image rotated -2deg.
- Sticker / badge at +5deg.
- Card hover effect: 1deg tilt.

```css
.hero-image { transform: rotate(-2deg); }
.badge { transform: rotate(5deg); }
```

### 2. Hand-drawn elements
- Underline that's a SVG squiggle, not a straight line.
- Arrows that look hand-drawn.
- Highlight that's a marker swipe, not a solid color.

### 3. Off-grid elements
- Image bleeds past container.
- Sticker / badge sits outside the card.
- Background shape extends beyond section.

### 4. Mixed sizes
- One card 2x bigger than others.
- One headline word 4x bigger.
- Variable line heights.

### 5. Asymmetric layouts
- Title left, content right (not both centered).
- 60/40 split, not 50/50.
- Off-center hero.

### 6. Texture
- Subtle paper texture.
- Grain overlay.
- Noise.

### 7. Variable type
- Different weights within a headline.
- Italic for emphasis (not bold).
- Mixed sans + serif (intentionally).

### 8. Imperfect illustrations
- Hand-drawn (not geometric).
- Slightly off-kilter.
- Custom (not stock).

---

## Examples

### Hero with rotated product screenshot
```jsx
<div className="relative">
  <img src="/product.png" className="-rotate-2 shadow-2xl" />
  <span className="absolute -top-4 -right-4 rotate-6 bg-yellow-300 px-3 py-1 rounded-full text-sm">
    New
  </span>
</div>
```

### Hand-drawn underline
```html
<span class="relative">
  Important
  <svg class="absolute -bottom-2 left-0 w-full" viewBox="0 0 100 10">
    <path d="M0 5 Q 25 0 50 5 T 100 5" stroke="currentColor" fill="none" />
  </svg>
</span>
```

### Bleeding image
```css
.hero-image {
  margin-right: -10%;  /* extends past container */
}
```

### Mixed weights in headline
```html
<h1>
  <span class="font-light">Ship</span>
  <span class="font-bold">faster</span>
  <span class="font-light italic">than ever</span>
</h1>
```

---

## Caveats

- Don't overdo it. One or two imperfections per page, not 20.
- Imperfection should feel intentional, not accidental.
- Brand-fit: a bank should be more restrained than a creative agency.

---

## The rule

If your design looks perfectly symmetric, perfectly aligned, perfectly consistent — add ONE imperfection. Just one. See how it feels.

---

**Next:** [before-after.md](before-after.md) · Back to [ANTI-AI-DESIGN/](README.md)
