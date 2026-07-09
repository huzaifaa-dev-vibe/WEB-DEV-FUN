# ACCESSIBILITY (Overview)

> Accessibility is not optional. This file is the overview; deep coverage in [Accessibility/](Accessibility/).

---

## Purpose

Make sure every user — including those with disabilities — can use what you build. Accessibility is also law (ADA, EAA, Section 508), good business (15–20% of users), and better SEO.

## Prerequisites

- Basic HTML, CSS, JS.
- A browser.

## Learning Outcome

You can build pages that pass WCAG 2.2 AA, work with keyboard and screen readers, and avoid the most common a11y failures.

## Related Files

- [Accessibility/](Accessibility/) — deep dives
- [COMMON_MISTAKES.md#accessibility](COMMON_MISTAKES.md)
- [Checklists/accessibility.md](Checklists/accessibility.md)
- [ANTI-AI-DESIGN/](ANTI-AI-DESIGN/) (some overlap)

## AI Instructions

When generating UI:
1. Use semantic HTML (`<button>`, `<nav>`, `<main>`, etc.). Don't `<div>` everything.
2. Every interactive element must be keyboard-accessible.
3. Every image needs `alt`. Decorative: `alt=""`. Informative: describe.
4. Every form input needs a `<label>`.
5. Color contrast ≥ 4.5:1 (normal text) / 3:1 (large/bold).
6. Don't disable `:focus-visible`.
7. Respect `prefers-reduced-motion`.
8. Test with axe DevTools before reporting done.

## Human Notes

Accessibility is not a checklist you bolt on at the end — it's how you build from the start. Fixing it later is 10x more expensive.

WCAG has 3 levels: A (minimum), AA (target), AAA (where possible). Aim for AA.

The POUR principles:
- **Perceivable** — users can perceive content (sight, hearing, touch).
- **Operable** — users can navigate and use.
- **Understandable** — content and UI make sense.
- **Robust** — works with assistive tech.

## Quick Wins

- Add `lang` attribute to `<html>`.
- Skip-to-content link as the first focusable element.
- One `<h1>` per page. Logical heading order.
- `:focus-visible` styled on every interactive element.
- `aria-label` on icon-only buttons.
- `aria-current` on the current nav item.
- `role="alert"` for important dynamic messages.
- Live regions for dynamic content (`aria-live`).
- Modal: focus trap, Esc to close, return focus on close.

## Tools

- **axe DevTools** — automated a11y audit.
- **Lighthouse** — built into Chrome.
- **WAVE** — https://wave.webaim.org/
- **NVDA / VoiceOver** — actual screen reader testing.
- **Stark** — Figma plugin + browser extension.
- **Pa11y** — CLI.
- **Accessibility Insights** — Microsoft's tool.

## References

- WCAG 2.2: https://www.w3.org/TR/WCAG22/
- ARIA Authoring Practices: https://www.w3.org/WAI/ARIA/apg/
- WebAIM: https://webaim.org/
- Inclusive Components: https://inclusive-components.design/
- a11yproject: https://www.a11yproject.com/

## Further Reading

- *Inclusive Components* — Heydon Pickering
- *Accessibility for Everyone* — Laura Kalbag
- *Web Accessibility: Web Standards and Regulatory Compliance* — Jim Thatcher et al.

## Exercises

1. Take a recent project. Run axe. Fix every issue.
2. Navigate your site with keyboard only. Note every friction point.
3. Use your site with VoiceOver/NVDA for 10 minutes.
4. Audit a popular site (Twitter, Amazon). Find 5 a11y issues.

## Projects

- Build an accessible modal (focus trap, return focus, Esc).
- Build an accessible dropdown menu (ARIA patterns).
- Build an accessible data table with sortable columns.

---

**Next:** [Accessibility/](Accessibility/) · [Performance](PERFORMANCE.md) · [SEO](SEO.md)
