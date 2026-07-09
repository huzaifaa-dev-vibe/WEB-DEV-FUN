# PERFORMANCE (Overview)

> Performance is a feature. The fastest sites win users, search, and revenue. Deep coverage in [Performance/](Performance/).

---

## Purpose

Make sites load fast, stay responsive, and feel snappy. Performance directly affects bounce rate, conversion, SEO, and user satisfaction.

## Prerequisites

- Basic understanding of browsers, HTTP, JS.

## Learning Outcome

You can measure performance, set budgets, hit Core Web Vitals targets, and debug slow pages.

## Related Files

- [Performance/](Performance/) — deep dives
- [WEB_VITALS.md](WEB_VITALS.md) — Core Web Vitals
- [Checklists/performance.md](Checklists/performance.md)
- [BEST_PRACTICES.md#performance](BEST_PRACTICES.md)

## AI Instructions

When building any UI:
1. Set performance budgets upfront. See [Performance/budgets.md](Performance/budgets.md).
2. Ship less JS. Question every dependency.
3. Images: AVIF/WebP, `srcset`, `loading="lazy"`, `width`/`height`.
4. Fonts: `font-display: swap`, `preload` critical, subset.
5. Code-split routes and below-fold components.
6. Use SSR/SSG where appropriate. → [Templates/_next-app/](Templates/)
7. Add caching headers. → [Performance/caching.md](Performance/caching.md)
8. Verify: Lighthouse ≥ 90 all categories. LCP < 2.5s, CLS < 0.1, INP < 200ms.

## Human Notes

Performance is measured, not guessed. Always start with measurement:
- **Lab data** (Lighthouse, WebPageTest) — synthetic, reproducible.
- **Field data** (CrUX, RUM) — what real users actually experience.

Both matter. Lab catches regressions; field catches reality.

The Core Web Vitals (2024):
- **LCP** (Largest Contentful Paint) — loading. Target < 2.5s.
- **CLS** (Cumulative Layout Shift) — visual stability. Target < 0.1.
- **INP** (Interaction to Next Paint) — interactivity. Target < 200ms. (Replaced FID in March 2024.)

Other vitals: TTFB, FCP, TBT.

## Quick Wins (in order of ROI)

1. **Images** — compress, modern format, responsive sizes. Often 50% of total bytes.
2. **JS** — code-split, lazy-load, replace heavy deps.
3. **Caching** — long max-age on static assets, CDN.
4. **Fonts** — `font-display: swap`, `preload`, subset.
5. **HTTP/2 or HTTP/3** — multiplexing, header compression.
6. **Preconnect / dns-prefetch** — for critical third-party origins.
7. **Critical CSS** — inline above-the-fold CSS.
8. **Tree-shaking** — remove unused exports.
9. **Compression** — Brotli > Gzip.
10. **Server response** — TTFB < 800ms.

## Anti-patterns

- Shipping 2MB of JS for a content site.
- 30 third-party scripts loading sync.
- Unoptimized images.
- No caching headers.
- Render-blocking CSS/JS in `<head>`.
- Layout shift from images/ads without dimensions.
- Client-side routing that re-fetches everything.

## Tools

- **Lighthouse** — built into Chrome DevTools.
- **PageSpeed Insights** — https://pagespeed.web.dev/
- **WebPageTest** — https://www.webpagetest.org/
- **GTmetrix** — https://gtmetrix.com/
- **CrUX Dashboard** — https://developer.chrome.com/docs/crux/
- **Bundlephobia** — https://bundlephobia.com/
- **Size Limit** — https://github.com/ai/size-limit
- **webpack-bundle-analyzer** / **rollup-plugin-visualizer**
- **Chrome DevTools Performance tab**
- **Chrome DevTools Memory tab**

## References

- web.dev/performance: https://web.dev/performance
- MDN Performance: https://developer.mozilla.org/en-US/docs/Web/Performance
- Chrome Performance blog: https://developer.chrome.com/blog/
- Patrick Meenan: https://twitter.com/patmeenan
- Addy Osmani: https://addyosmani.com/blog/

## Further Reading

- *High Performance Browser Networking* — Ilya Grigorik (free)
- *Web Performance in Action* — Jeremy Wagner
- *Image Optimization* — Addy Osmani

## Exercises

1. Pick a slow site (yours or a popular one). Run Lighthouse. Identify top 3 issues.
2. Reduce your own site's bundle by 30% without losing functionality.
3. Make your site load in <1s on Slow 3G.

## Projects

- Build a perf dashboard tracking LCP/CLS/INP over time.
- Optimize a Next.js app to 100/100/100/100 Lighthouse.
- Implement edge caching with Cloudflare.

---

**Next:** [Performance/](Performance/) · [WEB_VITALS.md](WEB_VITALS.md) · [SEO.md](SEO.md)
