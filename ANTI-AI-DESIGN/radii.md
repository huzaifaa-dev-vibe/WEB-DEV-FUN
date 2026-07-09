# Anti-AI-Design: Radii

> Mix radii intentionally. Not `rounded-2xl` on everything.

---

## The AI tell

`rounded-2xl` (16px) on every element: cards, buttons, inputs, images, modals, tooltips. Looks soft, samey, generic.

---

## Human approach

Mix radii by purpose:

| Element | Radius | Why |
|---|---|---|
| Inputs, small buttons | 4-6px (`rounded-md`) | Functional, dense |
| Cards, modals | 8-12px (`rounded-lg`) | Contained but not soft |
| Pills, tags, avatars | full (`rounded-full`) | Distinct shape |
| Large containers | 16-24px (`rounded-2xl`/`3xl`) | Soft for emphasis |
| Images | 0px (sharp) or 24px (very soft) | Pick a side, not middle |

---

## Patterns

### Pattern 1: Sharp + soft contrast
- Images: 0px (sharp)
- Cards: 12px
- Buttons: 6px
- Pills: full

### Pattern 2: All soft
- Everything: 12-16px
- Pills: full
- Use sparingly — can look samey.

### Pattern 3: All sharp (editorial)
- Everything: 0-4px
- Pills: full (for tags)
- Use for serious/editorial brands.

### Pattern 4: Mixed intentionally
- Hero image: 0px (bleeds)
- Product card: 16px (soft)
- CTA button: 8px
- Input: 6px
- Tag: full

---

## Rules

1. **Don't use one radius for everything.**
2. **Pick 2-3 radii, use consistently by purpose.**
3. **Pills/tags: always full.**
4. **Images: pick a side (sharp or very soft), not 8px middle.**
5. **Match radius to density** (dense UI = smaller radius).

---

## Examples

### Bad (AI)
- Card: `rounded-2xl`
- Button: `rounded-2xl`
- Input: `rounded-2xl`
- Avatar: `rounded-2xl` (instead of `rounded-full`)
- Image: `rounded-2xl`

### Good (human)
- Card: `rounded-lg` (8px)
- Button: `rounded-md` (6px)
- Input: `rounded-md` (6px)
- Avatar: `rounded-full`
- Image: `rounded-none` (sharp, bleeds)

---

**Next:** [icons.md](icons.md) · Back to [ANTI-AI-DESIGN/](README.md)
