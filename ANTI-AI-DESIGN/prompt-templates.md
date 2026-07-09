# Anti-AI-Design: Prompt Templates

> Prompts that produce human-looking UI (when given to Cursor / Claude / etc.).

---

## Prompt 1: Landing page (with anti-AI principles)

```
You are a senior design engineer.

Build a landing page for "<PRODUCT>".

PRODUCT: <one-sentence description>
AUDIENCE: <who>
VOICE: <casual technical / formal / playful>

MANDATORY READS (read before writing any code):
- /ANTI-AI-DESIGN/README.md
- /ANTI-AI-DESIGN/principles.md
- /ANTI-AI-DESIGN/hero-alternatives.md
- /ANTI-AI-DESIGN/checklist.md

Constraints:
- Stack: Next.js + Tailwind + shadcn/ui
- Pick a hero layout from hero-alternatives.md (NOT centered + 2 CTAs).
- Pick a palette from /Color-Palettes/ (NOT purple-pink gradient).
- Use Lucide icons (no emoji).
- Mix radii (don't use rounded-2xl everywhere).
- Vary spacing (don't use py-24 everywhere).
- Real copy (no lorem, no generic).
- Real product screenshots (use placeholder URLs that I'll replace).
- One intentional imperfection (slight rotation, asymmetric detail).
- Mobile-first. Test 375px.
- Accessibility: keyboard, focus-visible, contrast ≥ 4.5:1.
- Respect prefers-reduced-motion.

After writing, self-check against /ANTI-AI-DESIGN/checklist.md.
Fix all failures before reporting done.
```

---

## Prompt 2: Component (anti-AI)

```
You are a senior design engineer.

Build a "<COMPONENT>" component.

PURPOSE: <one sentence>
FRAMEWORK: <React/Vue/Svelte>
STYLING: Tailwind + shadcn/ui

MANDATORY READS:
- /ANTI-AI-DESIGN/README.md
- /ANTI-AI-DESIGN/radii.md
- /ANTI-AI-DESIGN/icons.md
- /ANTI-AI-DESIGN/motion.md
- /Accessibility/README.md

Constraints:
- Use Lucide icons (no emoji).
- Mix radii by purpose.
- Motion has purpose (state change, not decoration).
- If loading: skeleton (not spinner).
- If empty: explain + suggest action.
- If error: explain + suggest fix.
- Keyboard accessible.
- ARIA correct.
- prefers-reduced-motion respected.

Output:
- Component file.
- Test file (Vitest + Testing Library).
- 3-sentence design rationale citing the principles applied.
```

---

## Prompt 3: Audit (anti-AI)

```
You are a senior design lead.

Audit this UI for AI-generated tells:
<HTML_OR_SCREENSHOT>

MANDATORY READS:
- /ANTI-AI-DESIGN/checklist.md
- /ANTI-AI-DESIGN/principles.md

Run the checklist. For each fail, cite the principle violated and suggest a specific fix.

Also suggest 3 alternative layouts from /ANTI-AI-DESIGN/hero-alternatives.md (if hero).

Output:
- Score 0-10 (10 = looks human-designed).
- Top 5 tells (worst first) with specific fixes.
- 3 layout alternatives (if applicable).
- Verdict: ship / needs work / rework.
```

---

## Prompt 4: Copy rewrite

```
You are a senior copywriter.

Rewrite this copy to NOT sound AI-generated:

<CURRENT_COPY>

MANDATORY READS:
- /ANTI-AI-DESIGN/copywriting.md

Rules:
- Specific over generic.
- Concrete numbers.
- Active voice.
- Short.
- Talk like a person.
- Verb-led CTAs.
- No filler.
- No emoji in headlines.
- No "innovative", "cutting-edge", "seamless", "robust".

Output:
- Rewrite (headline, subhead, CTA).
- 1-sentence explanation of what changed and why.
```

---

## Prompt 5: Color palette picker

```
You are a senior brand designer.

Pick a color palette for "<PROJECT>".

PROJECT: <description>
BRAND PERSONALITY: <serious / playful / technical / warm / etc.>

MANDATORY READS:
- /ANTI-AI-DESIGN/color.md
- /Color-Palettes/README.md

Rules:
- NOT purple-to-pink gradient.
- Max 5 colors (bg, fg, muted, accent, surface).
- Use OKLCH.
- Contrast ≥ 4.5:1 for body.
- Dark mode variant.
- One accent color, used sparingly.

Output:
- Palette as CSS variables (light + dark).
- 1-sentence rationale per color choice.
- Where each color should be used.
```

---

## Using these prompts

1. Copy the template.
2. Fill placeholders.
3. Paste to Cursor / Claude / etc.
4. Verify against [checklist.md](checklist.md) after.

---

**Back to:** [ANTI-AI-DESIGN/](README.md) · [PROMPTS.md](../PROMPTS.md)
