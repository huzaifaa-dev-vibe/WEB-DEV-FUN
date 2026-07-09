# Anti-AI-Design: Icons

> No emoji as icons. Use a consistent SVG set.

---

## The AI tell

- 🚀 ⚡ 🎯 💡 🚀 as feature icons.
- Mixing icon sets (Lucide + Heroicons + Material).
- Random stroke widths.
- Different sizes within the same section.

---

## Human approach

### 1. Pick ONE icon set
- **Lucide** (default) — clean, 24×24, 2px stroke.
- **Phosphor** — multiple weights.
- **Heroicons** — Tailwind team.
- **Tabler** — 5000+ icons.

### 2. Be consistent
- Same stroke width within a section.
- Same size within a section.
- Same style (outline vs filled).

### 3. Use SVG, not fonts
- Inline SVG: control color via `currentColor`.
- Per-icon imports (tree-shakeable).
- Icon fonts (Font Awesome) are legacy.

### 4. Accessibility
- Decorative: `aria-hidden="true"`.
- Interactive (icon-only button): `aria-label`.

---

## Anti-patterns

### ❌ Emoji as icons
```
🚀 Lightning Fast
⚡ Secure
🎯 Precise
```
Looks cheap. Inconsistent rendering across platforms.

### ❌ Mixed sets
- Heroicons in nav.
- Lucide in cards.
- Tabler in footer.
Looks like 3 different designers.

### ❌ Different sizes
- 16px in nav.
- 20px in cards.
- 32px in hero.
For same-purpose icons.

### ❌ Different stroke widths
- Lucide (2px) next to Phosphor (1.5px).

---

## Good patterns

### ✅ Lucide everywhere, consistent
```jsx
import { Rocket, Shield, Target } from 'lucide-react';

<Feature icon={Rocket} title="Fast" />
<Feature icon={Shield} title="Secure" />
<Feature icon={Target} title="Precise" />
```

All 24×24, 2px stroke, same color (`currentColor`).

### ✅ Custom SVG for brand
- Hand-drawn or custom SVGs for hero illustrations.
- Same set throughout.

---

## When to use real photos instead

- For features that photos explain better (real product screenshots, real people using the product).
- For testimonial avatars (real customer photos).

---

## Icon resources

→ [Icons/](../Icons/) for full icon system guide.
→ [EXTERNAL_REPOSITORIES.md#icons](../EXTERNAL_REPOSITORIES.md#icons) for icon library list.

---

**Next:** [motion.md](motion.md) · Back to [ANTI-AI-DESIGN/](README.md)
