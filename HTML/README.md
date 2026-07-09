# HTML

> The semantic skeleton of the web. Get this right and half your accessibility, SEO, and structure problems disappear.

---

## Purpose

Teach you to write semantic, accessible, standards-compliant HTML that browsers, search engines, and assistive technologies all understand.

## Prerequisites

- Basic computer literacy.
- A text editor and browser.

## Learning Outcome

You can structure any web page using the right semantic element for the job, build accessible forms, and avoid div-soup.

## Dependencies

- None. This is the foundation.

## Related Files

- [CSS/](../CSS/) — styling
- [JavaScript/](../JavaScript/) — interactivity
- [Accessibility/](../Accessibility/) — a11y deep dive
- [SEO/](../SEO/) — search optimization
- [CHEATSHEET.md](../CHEATSHEET.md#html) — syntax quick-ref

## AI Instructions

When generating HTML:
1. Use semantic elements (`<article>`, `<nav>`, `<main>`, `<section>`, `<aside>`, `<header>`, `<footer>`, `<figure>`, `<details>`) over `<div>` where appropriate.
2. Use the correct input type (`email`, `tel`, `url`, `number`, `date`, `color`, `range`).
3. Every input has a `<label>` (via `for`/`id` or wrapping).
4. Every image has `alt` (decorative: `alt=""`).
5. Every image has `width` and `height` (prevents CLS).
6. Use `loading="lazy"` on below-fold images.
7. Use `fetchpriority="high"` on the LCP image.
8. One `<h1>` per page. Logical heading order.
9. Use `<a>` for navigation, `<button>` for actions. Don't `<div onclick>`.
10. Add `rel="noopener noreferrer"` on `target="_blank"` links.
11. Use the `<dialog>` element for modals.
12. Use `<details>`/`<summary>` for accordions before reaching for JS.
13. Validate at https://validator.w3.org/

## Human Notes

HTML is the most forgiving language on the web. Browsers will render almost anything. That forgiveness is a trap — sloppy HTML still "works" but breaks accessibility, SEO, and maintenance.

Key principles:
- **Semantics over appearance.** Choose elements by meaning, not by how they look. Style with CSS.
- **Native first.** Before reaching for a JS component, check if HTML has a native solution (`<details>`, `<dialog>`, `<progress>`, `<meter>`, `<datalist>`).
- **Structure matters.** Use heading levels to create a document outline. Screen reader users navigate by headings.
- **Forms are hard.** Most forms on the web suck. Spend time on labels, errors, and keyboard flow.

## Document Skeleton

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Page description for SEO and social sharing.">
  <title>Page Title | Site Name</title>

  <link rel="icon" href="/favicon.ico" sizes="any">
  <link rel="icon" href="/icon.svg" type="image/svg+xml">
  <link rel="apple-touch-icon" href="/apple-touch-icon.png">
  <link rel="manifest" href="/manifest.webmanifest">

  <meta property="og:title" content="Page Title">
  <meta property="og:description" content="Page description.">
  <meta property="og:image" content="https://example.com/og.png">
  <meta property="og:url" content="https://example.com/page">
  <meta name="twitter:card" content="summary_large_image">

  <link rel="canonical" href="https://example.com/page">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preload" as="image" href="/hero.webp" fetchpriority="high">
</head>
<body>
  <a href="#main" class="skip-link">Skip to content</a>
  <header>
    <nav aria-label="Main">
      <ul>
        <li><a href="/" aria-current="page">Home</a></li>
        <li><a href="/about">About</a></li>
      </ul>
    </nav>
  </header>
  <main id="main">
    <article>
      <h1>Page Title</h1>
      <p>Content...</p>
    </article>
    <aside aria-label="Related">
      <!-- sidebar -->
    </aside>
  </main>
  <footer>
    <p>&copy; 2025 Site Name</p>
  </footer>
</body>
</html>
```

## Semantic Elements Cheatsheet

| Element | Use for |
|---|---|
| `<header>` | Intro of a page, article, or section. Often contains nav/logo. |
| `<nav>` | Major navigation blocks. Don't wrap every list of links. |
| `<main>` | The main content. One per page. |
| `<article>` | Self-contained content (blog post, card, comment). |
| `<section>` | Thematic grouping with a heading. |
| `<aside>` | Tangentially related content (sidebar, pull quote). |
| `<footer>` | End of a page/article/section. |
| `<figure>` + `<figcaption>` | Image / code / quote with caption. |
| `<time datetime="2025-01-15">` | Dates / times (machine-readable). |
| `<address>` | Contact info for the article author. |
| `<mark>` | Highlighted text. |
| `<details>` + `<summary>` | Disclosure widget (no JS needed). |
| `<dialog>` | Modal (with `showModal()`). |
| `<progress>` | Progress bar. |
| `<meter>` | Gauge (e.g., disk usage). |

## Forms

```html
<form action="/submit" method="POST" novalidate>
  <fieldset>
    <legend>Account</legend>

    <div class="field">
      <label for="name">Name <span aria-hidden="true">*</span></label>
      <input id="name" name="name" type="text" required autocomplete="name">
      <small id="name-hint">As it appears on your ID.</small>
    </div>

    <div class="field">
      <label for="email">Email</label>
      <input id="email" name="email" type="email" required autocomplete="email">
    </div>

    <div class="field">
      <label for="password">Password</label>
      <input id="password" name="password" type="password" required minlength="8" autocomplete="new-password">
    </div>

    <div class="field">
      <label for="country">Country</label>
      <select id="country" name="country">
        <option value="">Select...</option>
        <option value="us">United States</option>
        <option value="uk">United Kingdom</option>
      </select>
    </div>

    <div class="field">
      <label>
        <input type="checkbox" name="agree" required>
        I agree to the terms
      </label>
    </div>

    <button type="submit">Create account</button>
  </fieldset>
</form>
```

Form principles:
- Always `<label>`. Always.
- Use the right `type` (triggers mobile keyboards, validation).
- Use `autocomplete` properly: https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/autocomplete
- Use `inputmode` for fine-tuned mobile keyboards.
- Use `pattern` for custom validation. Don't forget error messages.
- Validate on the server too. Client validation is UX, not security.
- Use `fieldset`/`legend` to group related fields.

## Accessibility Primitives

- `aria-label` — when text isn't visible (icon button).
- `aria-labelledby` — when label is elsewhere on the page.
- `aria-describedby` — for hints/errors.
- `aria-live="polite"` — for non-critical dynamic content.
- `aria-live="assertive"` — for critical alerts.
- `role="alert"` — for important immediate messages.
- `aria-current="page"` — current nav item.
- `aria-expanded` — for collapsible sections.
- `aria-hidden="true"` — hide from AT (decorative icons).

Don't overuse ARIA. The first rule of ARIA: don't use ARIA. Use native HTML when possible.

## Common Mistakes

- ❌ `<div onclick>` for buttons.
- ❌ `<span>` for links.
- ❌ Missing `<label>`.
- ❌ Missing `alt`.
- ❌ Missing `width`/`height` on images.
- ❌ Multiple `<h1>` per page.
- ❌ Heading levels skipped (h1 → h3).
- ❌ `<br>` for spacing.
- ❌ `<b>`/`<i>` for bold/italic (use `<strong>`/`<em>` for semantics, CSS for visuals).
- ❌ Inline `style="..."` everywhere.

→ [COMMON_MISTAKES.md#html--markup](../COMMON_MISTAKES.md)

## References

- MDN HTML: https://developer.mozilla.org/en-US/docs/Web/HTML
- HTML Spec (WHATWG): https://html.spec.whatwg.org/
- HTML Reference: https://htmlreference.io/
- W3C Validator: https://validator.w3.org/
- HTML5 Doctor: http://html5doctor.com/
- Web.dev HTML: https://web.dev/learn/html

## Further Reading

- *HTML5 Up and Running* — Mark Pilgrim (free: https://diveinto.html5doctor.com/)
- MDN HTML guide

## Exercises

1. Build a complete blog post page using only semantic HTML. No CSS.
2. Build an accessible registration form (5 fields, validation, error states).
3. Convert a `<div>`-based page to semantic HTML. Compare a11y.
4. Validate your site at https://validator.w3.org/. Fix all errors.

## Projects

- Build a semantic news article template.
- Build a multi-step accessible form (with progress).
- Build a tabbed interface using only `<details>` and CSS.

---

**Previous:** [START-HERE.md](../START-HERE.md) · **Next:** [CSS/](../CSS/) · **Related:** [Accessibility/](../Accessibility/), [SEO/](../SEO/)
