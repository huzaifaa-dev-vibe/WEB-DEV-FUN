# WEB VITALS

> The metrics that matter. If you only track 3 things, track these.

---

## Purpose

Define the user-experience metrics Google uses to rank sites and that engineers use to optimize them.

## Prerequisites

- Basic browser/rendering understanding.

## Learning Outcome

You can measure LCP, CLS, INP, know what causes them to be poor, and know how to fix them.

## Related Files

- [Performance/](Performance/)
- [SEO.md](SEO.md)
- [Checklists/performance.md](Checklists/performance.md)

## AI Instructions

When shipping any page:
1. Measure LCP, CLS, INP (Lighthouse + field data).
2. If any metric fails target, identify cause, fix, re-measure.
3. Targets: LCP < 2.5s, CLS < 0.1, INP < 200ms.

## Human Notes

Core Web Vitals are Google's subset of Web Vitals — the metrics they consider essential. They've evolved:

- **2020–2024 (Mar):** LCP, FID, CLS
- **March 2024+:** LCP, **INP** (replaced FID), CLS

Google ranks on the **field data** from real Chrome users (CrUX), not your lab data. But lab data catches regressions before they hit production.

---

## The Big Three

### LCP (Largest Contentful Paint)
**Measures:** loading. When the largest visible element finishes rendering.
**Target:** < 2.5s at the 75th percentile.
**Common causes:**
- Slow server response (TTFB).
- Render-blocking JS/CSS.
- Large image (often the hero) without `srcset` or `fetchpriority="high"`.
- Web fonts blocking text.
- Client-side rendering without streaming.

**Fixes:**
- Optimize server (SSR, edge, cache).
- Preload hero image: `<link rel="preload" as="image" href="..." fetchpriority="high">`.
- `font-display: swap`.
- Critical CSS inlined.
- Reduce JS, code-split.
- Use modern image formats.

### CLS (Cumulative Layout Shift)
**Measures:** visual stability. Sum of layout shifts.
**Target:** < 0.1.
**Common causes:**
- Images/ads/embeds without `width` and `height`.
- Web fonts causing FOUT/FOIT.
- Dynamically injected content above the fold.
- Animations on `width`/`height`/`top`/`left`.

**Fixes:**
- Always specify `width` and `height` on images.
- Reserve space for ads/embeds.
- Use `font-display: swap` + size-adjust to match fallback font.
- Don't insert content above current scroll position.
- Animate `transform`/`opacity`, not layout.

### INP (Interaction to Next Paint)
**Measures:** responsiveness. Time from user input to next paint, across all interactions. Reports the worst (well, 98th percentile).
**Target:** < 200ms. (< 500ms is "needs improvement"; > 500ms is "poor".)
**Common causes:**
- Long JS tasks blocking the main thread.
- Heavy event handlers.
- Synchronous re-renders.
- Long network requests in click handlers.
- Third-party scripts.

**Fixes:**
- Break long tasks (`setTimeout`, `scheduler.yield()`, Web Workers).
- Debounce/throttle expensive handlers.
- Memoize, virtualize long lists.
- Defer non-critical JS.
- Use React Server Components / streaming.
- Reduce third-party scripts.

---

## Other Important Vitals

### TTFB (Time to First Byte)
- Time from request to first byte received.
- Target: < 800ms.
- Cause: slow server, slow DB, no CDN, cold start.
- Fix: edge cache, CDN, optimize queries, pre-render.

### FCP (First Contentful Paint)
- Time until first text/image is painted.
- Target: < 1.8s.
- Cause: render-blocking resources.
- Fix: inline critical CSS, defer JS, preload fonts.

### TBT (Total Blocking Time)
- Lab-only. Total time the main thread was blocked.
- Target: < 200ms.
- Cause: long JS tasks.
- Fix: same as INP.

### Speed Index
- How quickly content is visually displayed.
- Target: < 3.4s.

---

## How to Measure

### Lab (synthetic)
- **Lighthouse** — runs in Chrome DevTools.
- **PageSpeed Insights** — web-based Lighthouse.
- **WebPageTest** — most configurable.
- **Custom Lighthouse CI** — in your CI pipeline.

### Field (real users)
- **CrUX** — Chrome UX Report (public dataset).
- **RUM** (Real User Monitoring) — your own beacon.
- **web-vitals** library — https://github.com/GoogleChrome/web-vitals

```js
import { onLCP, onCLS, onINP } from 'web-vitals';

onLCP(console.log);
onCLS(console.log);
onINP(console.log);
```

Send to your analytics. → [Performance/rum.md](Performance/rum.md)

---

## Targets Summary

| Metric | Good | Needs improvement | Poor |
|---|---|---|---|
| LCP | < 2.5s | 2.5–4.0s | > 4.0s |
| INP | < 200ms | 200–500ms | > 500ms |
| CLS | < 0.1 | 0.1–0.25 | > 0.25 |
| FCP | < 1.8s | 1.8–3.0s | > 3.0s |
| TTFB | < 800ms | 800–1800ms | > 1800ms |

---

## AI Agent Verification

When an AI agent reports a UI "done", they MUST include:

```
Lighthouse (mobile):
- Performance: __
- Accessibility: __
- Best Practices: __
- SEO: __

Core Web Vitals:
- LCP: __ ms
- CLS: __
- INP: __ ms

Field data (if available): <link to CrUX or RUM dashboard>
```

If any metric is below target, the UI is not done.

## References

- https://web.dev/articles/vitals
- https://web.dev/articles/lcp
- https://web.dev/articles/cls
- https://web.dev/articles/inp
- https://web.dev/articles/ttfb
- https://developer.chrome.com/docs/crux/

## Further Reading

- *Image Optimization* — Addy Osmani
- *High Performance Browser Networking* — Ilya Grigorik

## Exercises

1. Install `web-vitals` on a site. Log metrics to console.
2. Take a slow page. Profile each Core Web Vital. Find the cause.
3. Improve LCP by 1s on a real page.

## Projects

- Build a RUM collector that stores vitals in Postgres + visualizes in Grafana.
- Set up Lighthouse CI in GitHub Actions. Block merges on regressions.

---

**Next:** [Performance/](Performance/) · [SEO.md](SEO.md) · [Checklists/](Checklists/)
