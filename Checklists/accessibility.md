# Accessibility Checklist

> Run on every UI change.

## Semantic HTML
- [ ] Use semantic elements (`<nav>`, `<main>`, `<article>`, `<section>`, `<aside>`, `<header>`, `<footer>`, `<figure>`).
- [ ] One `<h1>` per page.
- [ ] Logical heading order (no skipping levels).
- [ ] `<button>` for actions, `<a>` for navigation.
- [ ] No `<div onclick>` for interactive elements.

## Forms
- [ ] Every input has a `<label>`.
- [ ] Required fields marked.
- [ ] Error messages linked via `aria-describedby`.
- [ ] `aria-invalid="true"` on errored fields.
- [ ] Group with `<fieldset>`/`<legend>`.
- [ ] Sensible autocomplete attrs.
- [ ] Validate on blur (not every keystroke).

## Images & Media
- [ ] Every image has `alt`.
  - Decorative: `alt=""`.
  - Informative: describe.
  - Chart: summarize.
- [ ] `<figcaption>` for figures.
- [ ] Captions / transcripts for video.
- [ ] No autoplay.
- [ ] Audio controls visible.

## Keyboard
- [ ] All interactive elements reachable by Tab.
- [ ] Logical tab order.
- [ ] `:focus-visible` styled.
- [ ] No keyboard traps.
- [ ] Modal: focus trap + Esc + return focus.
- [ ] Dropdown: arrow keys + Esc.
- [ ] Tabs: arrow keys.

## Color & Contrast
- [ ] Body text ≥ 4.5:1.
- [ ] Large text ≥ 3:1.
- [ ] UI components (borders, icons) ≥ 3:1.
- [ ] Don't rely on color alone (use text + icon).
- [ ] Test with color blindness simulator.

## ARIA
- [ ] Use ARIA only when native HTML can't.
- [ ] `aria-label` on icon-only buttons.
- [ ] `aria-current` on current nav item.
- [ ] `aria-expanded` on collapsibles.
- [ ] `aria-live` for dynamic content.
- [ ] `role="alert"` for immediate alerts.
- [ ] Hide decorative elements with `aria-hidden="true"`.

## Motion
- [ ] `prefers-reduced-motion` respected.
- [ ] No autoplaying motion.
- [ ] No flashing > 3x/sec.
- [ ] Parallax optional or removed.

## Screen Reader
- [ ] Tested with VoiceOver (macOS) or NVDA (Windows).
- [ ] Page makes sense when read aloud.
- [ ] Skip-to-content link present.
- [ ] `lang` attribute on `<html>`.

## Tools
- [ ] axe DevTools: 0 issues.
- [ ] Lighthouse a11y ≥ 95.
- [ ] WAVE: 0 errors.
- [ ] Keyboard-only test passed.

## References
- WCAG 2.2: https://www.w3.org/TR/WCAG22/
- ARIA Authoring Practices: https://www.w3.org/WAI/ARIA/apg/

---

**Next:** [performance.md](performance.md) · Back to [Checklists/](README.md)
