# Accessibility

> Accessibility is not optional. Build for everyone or build for no one.

---

## Purpose

Make sure every user — including those with disabilities — can use what you build. Accessibility is also law (ADA, EAA, Section 508), good business, and better SEO.

## Prerequisites

- [HTML/](../HTML/), [CSS/](../CSS/).

## Learning Outcome

You can build pages that pass WCAG 2.2 AA, work with keyboard and screen readers, and avoid the most common a11y failures.

## Dependencies

- HTML/CSS.

## Related Files

- [HTML/](../HTML/) · [CSS/](../CSS/) · [ACCESSIBILITY.md](../ACCESSIBILITY.md) (overview) · [Checklists/accessibility.md](../Checklists/accessibility.md) · [COMMON_MISTAKES.md#accessibility](../COMMON_MISTAKES.md)

## AI Instructions

When generating UI:
1. Use semantic HTML first. ARIA only when native won't work.
2. Every interactive element must be keyboard-accessible.
3. Every image needs `alt`. Decorative: `alt=""`.
4. Every form input needs a `<label>`.
5. Color contrast ≥ 4.5:1 (normal text) / 3:1 (large/bold).
6. Don't disable `:focus-visible`.
7. Respect `prefers-reduced-motion`.
8. Modals: focus trap, return focus, Esc to close.
9. Test with axe DevTools before reporting done.
10. Don't fake interaction with `div`+`onclick`. Use `<button>`/`<a>`.

## Human Notes

### WCAG Principles (POUR)
- **Perceivable** — content must be presentable in ways users can perceive.
- **Operable** — interface must be operable (keyboard, etc.).
- **Understandable** — content and operation must be understandable.
- **Robust** — content must work with assistive technologies.

### Levels
- **A** — minimum.
- **AA** — target for most sites.
- **AAA** — where possible.

### Disabilities to design for
- Vision (blind, low vision, color blindness).
- Hearing (deaf, hard of hearing).
- Motor (cannot use mouse, tremors).
- Cognitive (ADHD, dyslexia, memory).
- Vestibular (motion sensitivity).
- Speech (use AAC devices).
- Temporary (broken arm, lost glasses).
- Situational (bright sunlight, noisy room, holding a baby).

## Keyboard Navigation

- Tab order matches visual order (mostly).
- Skip link as first focusable element.
- Visible `:focus-visible` style on every interactive element.
- All functionality available via keyboard.
- No keyboard traps (except intentional, like modals).
- Logical tab order (don't reorder with `tabindex`).

```css
/* Visible focus */
:focus-visible {
  outline: 2px solid var(--color-accent);
  outline-offset: 2px;
}

/* Skip link */
.skip-link {
  position: absolute;
  top: -100px;
  left: 0;
  background: white;
  padding: 1rem;
  z-index: 1000;
}
.skip-link:focus {
  top: 0;
}
```

## Screen Readers

Test with:
- **NVDA** (Windows, free) — https://www.nvda-project.org/
- **VoiceOver** (macOS/iOS, built-in) — Cmd+F5 to toggle.
- **TalkBack** (Android, built-in).
- **JAWS** (Windows, paid, enterprise).

Key screen reader behaviors:
- Navigate by heading (H key).
- Navigate by landmark (D key).
- Read form labels (F key).
- List links (U key).

## ARIA (use sparingly)

> The first rule of ARIA: don't use ARIA. — W3C

ARIA is for when native HTML can't express what you need. Common patterns:

### `aria-label` (no visible text)
```html
<button aria-label="Close dialog">
  <svg>...</svg>
</button>
```

### `aria-labelledby` (label is elsewhere)
```html
<h2 id="section-title">Settings</h2>
<section aria-labelledby="section-title">...</section>
```

### `aria-describedby` (extra info)
```html
<label for="password">Password</label>
<input id="password" type="password" aria-describedby="pw-hint">
<small id="pw-hint">Min 8 chars, 1 number.</small>
```

### `aria-live` (dynamic content)
```html
<div aria-live="polite" id="status"></div>
<div aria-live="assertive" id="alert"></div>
```

### `role="alert"` (immediate alert)
```html
<div role="alert">Your session is expiring.</div>
```

### `aria-current`
```html
<a href="/" aria-current="page">Home</a>
```

### `aria-expanded`, `aria-controls`
```html
<button aria-expanded="false" aria-controls="menu" onclick="toggle()">Menu</button>
<ul id="menu" hidden>...</ul>
```

## Common Patterns

### Modal
```html
<dialog open aria-labelledby="modal-title">
  <h2 id="modal-title">Confirm</h2>
  <p>Are you sure?</p>
  <button>Yes</button>
  <button>No</button>
</dialog>
```
- Use `<dialog>` element.
- Trap focus inside.
- Return focus to trigger on close.
- Esc to close.
- Click backdrop to close (optional).

### Tabs (ARIA pattern)
```html
<div role="tablist">
  <button role="tab" id="tab-1" aria-selected="true" aria-controls="panel-1">Tab 1</button>
  <button role="tab" id="tab-2" aria-selected="false" aria-controls="panel-2" tabindex="-1">Tab 2</button>
</div>
<div role="tabpanel" id="panel-1" aria-labelledby="tab-1">Content 1</div>
<div role="tabpanel" id="panel-2" aria-labelledby="tab-2" hidden>Content 2</div>
```
→ https://www.w3.org/WAI/ARIA/apg/patterns/tabs/

### Accordion
Use native `<details>`/`<summary>` first.

### Combobox / Autocomplete
Complex. Follow the ARIA pattern: https://www.w3.org/WAI/ARIA/apg/patterns/combobox/

### Toast / Notifications
```html
<div role="status" aria-live="polite">Saved successfully.</div>
<div role="alert" aria-live="assertive">Connection lost.</div>
```

## Color Contrast

| Text size | Min contrast |
|---|---|
| Normal text (< 18pt or < 14pt bold) | 4.5:1 |
| Large text (≥ 18pt or ≥ 14pt bold) | 3:1 |
| UI components (borders, icons) | 3:1 |

Test with:
- WebAIM Contrast Checker: https://webaim.org/resources/contrastchecker/
- Who Can Use: https://www.whocanuse.com/
- axe DevTools.

## Forms Accessibility

- Every input has a `<label>`.
- Group with `<fieldset>`/`<legend>`.
- Required fields: `required` attribute (also conveys to AT).
- Error messages: `aria-invalid="true"` and `aria-describedby` pointing to error.
- Don't disable submit until valid (or explain why).
- Don't auto-advance fields.
- Don't submit on blur without warning.

## Motion & Vestibular

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

Also avoid:
- Auto-playing video.
- Parallax.
- Auto-advancing carousels.
- Flashing > 3 times/sec (seizure risk).

## Common A11y Failures

1. **Low contrast text.** (Most common failure on the web.)
2. **Missing `alt` on images.**
3. **Missing form labels.**
4. **Empty links / buttons.**
5. **Missing `lang` attribute.**
6. **No keyboard navigation.**
7. **`<div onclick>` for buttons.**
8. **No `:focus-visible` style.**
9. **Modal without focus trap.**
10. **Auto-playing media.**

## Tools

- **axe DevTools** (browser extension) — best automated checker.
- **Lighthouse** — built into Chrome, includes a11y.
- **WAVE** — https://wave.webaim.org/
- **Pa11y** — CLI for CI.
- **Accessibility Insights** (Microsoft) — https://accessibilityinsights.io/
- **Stark** — Figma plugin + browser extension.
- **headless keyboard testing** — `chrome --force-renderer-accessibility`.

## Audit Process

1. **Automated** — axe / Lighthouse. Catches ~30-50% of issues.
2. **Keyboard** — unplug mouse. Use only keyboard.
3. **Screen reader** — NVDA / VoiceOver. Navigate the page.
4. **Manual** — visual inspection (contrast, font size, zoom 200%, etc.).
5. **User testing** — with actual users with disabilities.

## References

- WCAG 2.2: https://www.w3.org/TR/WCAG22/
- ARIA Authoring Practices: https://www.w3.org/WAI/ARIA/apg/
- WebAIM: https://webaim.org/
- Inclusive Components: https://inclusive-components.design/
- A11y Project: https://www.a11yproject.com/
-Deque: https://www.deque.com/blog/

## Further Reading

- *Inclusive Components* — Heydon Pickering (free)
- *Accessibility for Everyone* — Laura Kalbag
- *Web Accessibility: Web Standards and Regulatory Compliance* — Jim Thatcher et al.

## Exercises

1. Take a recent project. Run axe. Fix every issue.
2. Navigate your site with keyboard only. Note every friction.
3. Use your site with VoiceOver / NVDA for 10 minutes.
4. Audit a popular site (Twitter, Amazon). Find 5 a11y issues.

## Projects

- Build an accessible modal (focus trap, return focus, Esc, backdrop click).
- Build an accessible dropdown menu using ARIA pattern.
- Build an accessible sortable data table.

---

**Previous:** [HTML/](../HTML/) · **Next:** [Responsive-Design/](../Responsive-Design/) · **Related:** [CSS/](../CSS/), [Checklists/](../Checklists/)
