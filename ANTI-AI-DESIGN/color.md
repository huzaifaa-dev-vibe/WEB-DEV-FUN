# Anti-AI-Design: Color

> Color usage that doesn't scream AI.

---

## The AI color tells

1. **Purple-to-pink gradient** (the most obvious).
2. **Vercel blue** (`#0070f3`) used everywhere because Vercel uses it.
3. **Tailwind default palette** without modification.
4. **Same color for everything** (one accent for buttons, links, headlines, focus states).
5. **Black + white + one Tailwind color** with no thought.
6. **Glassmorphism** (`backdrop-blur` over gradient).
7. **Rainbow gradient text** on hero headlines.

---

## Human color choices

### 1. Pick a palette with intent
- Use [Color-Palettes/](../Color-Palettes/) for curated sets.
- Choose by brand personality, not by trend.
- Limit to 3-5 colors total: bg, fg, muted, accent, surface.

### 2. Avoid the gradient
- Solid colors > gradients almost always.
- If gradient, use 2 colors that aren't purple-pink.
- Subtle is fine. Rainbow is not.

### 3. Use OKLCH
- Perceptually uniform.
- Easier to make accessible.
- `oklch(60% 0.2 250)` not `rebeccapurple`.

### 4. Vary by purpose
- Primary accent: brand color.
- Secondary accent: complementary or muted.
- Success: green (but a specific green, not Tailwind's).
- Warning: amber.
- Error: red.
- Info: blue.

### 5. Use neutrals intentionally
- Don't use pure black (`#000000`) — too harsh.
- Use `#0a0a0a` or `#18181b` for dark text.
- Use `#fafafa` or `#f4f4f5` for light bg.
- Tint neutrals slightly with your accent (e.g., warm gray for warm palette).

### 6. Test contrast
- 4.5:1 minimum for body text.
- 3:1 for large text.
- Use WebAIM or Who Can Use.

### 7. Dark mode
- Not just inverted. Real dark mode palette.
- Use `oklch` and reduce lightness, not just invert.
- Test in both.

---

## Palette ideas (not purple-pink)

### Editorial / serious
- Bg: `#fafaf9` (warm white)
- Fg: `#1c1917` (warm black)
- Accent: `#9f1239` (deep rose)
- Muted: `#78716c` (warm gray)

### Tech / modern
- Bg: `#0a0a0a`
- Fg: `#fafafa`
- Accent: `#22d3ee` (cyan)
- Muted: `#737373`

### Warm / friendly
- Bg: `#fffbeb` (cream)
- Fg: `#1c1917`
- Accent: `#ea580c` (orange)
- Muted: `#78716c`

### Minimal / Swiss
- Bg: `#ffffff`
- Fg: `#000000`
- Accent: `#dc2626` (red)
- Muted: `#525252`

### Healthcare / clean
- Bg: `#f0f9ff` (light blue)
- Fg: `#0c4a6e`
- Accent: `#0284c7`
- Muted: `#94a3b8`

### Fintech / trustworthy
- Bg: `#0f172a` (dark navy)
- Fg: `#f8fafc`
- Accent: `#10b981` (emerald)
- Muted: `#94a3b8`

### Education / playful
- Bg: `#fefce8`
- Fg: `#1c1917`
- Accent: `#7c3aed` (purple — okay here because not gradient)
- Muted: `#78716c`

### Gaming / vibrant
- Bg: `#0a0a0a`
- Fg: `#fafafa`
- Accent: `#84cc16` (lime)
- Muted: `#737373`

### AI / future (without being AI-tell)
- Bg: `#0a0a0a`
- Fg: `#fafafa`
- Accent: `#06b6d4` (cyan) or `#a3e635` (lime)
- Muted: `#737373`

---

## When gradient IS okay

- Logo mark.
- Subtle background texture (very low opacity).
- Single accent button (subtle hue shift, not rainbow).
- Hero photo overlay (for text legibility).

When NOT okay:
- Hero headline text fill.
- Body text.
- Background of every section.
- Cards.

---

## Real-world examples (study these)

- Linear: dark, restrained, single accent (purple, but used sparingly).
- Stripe: clean, varied gradients (subtle, brand-consistent).
- Vercel: black + white + occasional blue.
- Apple: white + black + product colors.
- Notion: warm whites, subtle accent.
- Figma: colorful but used purposefully.

Note: even Linear uses purple. The tell isn't "purple exists", it's "purple-to-pink gradient as hero background".

---

**Next:** [typography.md](typography.md) · Back to [ANTI-AI-DESIGN/](README.md)
