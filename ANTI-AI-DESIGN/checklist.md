# Anti-AI-Design: Checklist

> Run this checklist before shipping any UI. Fix every failure.

---

## Hero
- [ ] Hero is NOT centered text + 2 CTAs + 3 feature cards.
- [ ] Hero layout picked from [hero-alternatives.md](hero-alternatives.md).
- [ ] No "Powered by AI" badge.

## Color
- [ ] No purple-to-pink gradient as background.
- [ ] No rainbow gradient on headline text.
- [ ] Palette is intentional (max 5 colors).
- [ ] Contrast ≥ 4.5:1 for body text.
- [ ] Dark mode is real, not just inverted.

## Typography
- [ ] Max 2 typefaces (1 + display).
- [ ] Type scale uses `rem` and `clamp()`.
- [ ] No `<br>` for spacing.
- [ ] No `text-3xl font-bold` everywhere.
- [ ] Line height is 1.5+ for body.
- [ ] Max measure (line length) is 60-80 chars.

## Radii
- [ ] Radii are mixed (small / medium / large / full).
- [ ] Not `rounded-2xl` on everything.
- [ ] Radii chosen by purpose, not by default.

## Icons
- [ ] NO emoji as icons.
- [ ] Using a consistent icon set (Lucide / Phosphor / etc.).
- [ ] All icons same stroke width.
- [ ] All icons same size within a section.

## Copy
- [ ] NO "lorem ipsum" anywhere.
- [ ] NO generic copy ("We provide innovative solutions").
- [ ] Headlines are specific.
- [ ] CTAs are action verbs ("Start free trial" not "Click here").
- [ ] Voice is consistent.

## Testimonials
- [ ] NO fake testimonials with stock photos + 5 stars.
- [ ] Either real testimonials (with permission) or omit the section.

## Photography
- [ ] NO "diverse team laughing at laptop" stock.
- [ ] NO Unsplash random mountains.
- [ ] Real product screenshots.
- [ ] Real team photos (or no team photos).
- [ ] Real customer photos (or initials/avatars).

## Motion
- [ ] NO `fade-in-up` on every section.
- [ ] NO auto-rotating carousels.
- [ ] NO parallax for its own sake.
- [ ] Motion explains state (modal open, list reorder).
- [ ] `prefers-reduced-motion` respected.

## Spacing
- [ ] Spacing varies between sections (not all `py-24`).
- [ ] Asymmetric where appropriate.
- [ ] Mobile spacing is comfortable (not cramped).

## Layout
- [ ] NOT a generic 3-column card grid (unless intentional).
- [ ] Some sections break the grid.
- [ ] Some elements bleed off edges.
- [ ] Density varies (not every section breathes the same).

## Voice / Personality
- [ ] The site has a personality.
- [ ] A senior designer would NOT immediately say "AI made this".
- [ ] One element of imperfection (slight rotation, asymmetric detail, hand-drawn element).

## Accessibility (non-negotiable)
- [ ] All interactive elements keyboard-accessible.
- [ ] `:focus-visible` styled.
- [ ] All images have `alt`.
- [ ] All inputs have `<label>`.
- [ ] Color contrast passes (axe / Lighthouse).
- [ ] Heading order logical.
- [ ] Reduced motion respected.

## Performance (non-negotiable)
- [ ] Lighthouse mobile ≥ 90.
- [ ] LCP < 2.5s.
- [ ] CLS < 0.1.
- [ ] INP < 200ms.
- [ ] Images optimized (AVIF/WebP, srcset, lazy).

## Real content
- [ ] All copy is real (or clearly marked as placeholder for client).
- [ ] All images are real or intentionally absent.
- [ ] No "lorem", "test", "foo", "bar", "John Doe", "Jane Smith" in shipping code.

---

## Scoring

- 0-5 failures: looks human. Ship.
- 6-10 failures: needs work. Fix before shipping.
- 11+ failures: looks AI-generated. Rework.

---

## AI Agent: Mandatory

If you are an AI agent generating UI, you MUST:
1. Read this checklist.
2. Generate the UI.
3. Self-check against this checklist.
4. Fix all failures.
5. Re-check.
6. Then report done.

Skipping this checklist = the UI is not done.

---

**Next:** [principles.md](principles.md) · Back to [ANTI-AI-DESIGN/](README.md)
