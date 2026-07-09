# Performance

> Performance is a feature. The fastest sites win.

---

## Purpose

Make sites load fast, stay responsive, and feel snappy.

## Prerequisites

- Browser basics, [JavaScript/](../JavaScript/).

## Learning Outcome

You can measure, set budgets, hit Core Web Vitals, and debug slow pages.

## Dependencies

- DevTools.

## Related Files

- [PERFORMANCE.md](../PERFORMANCE.md) · [WEB_VITALS.md](../WEB_VITALS.md) · [Performance/budgets.md](budgets.md) · [Performance/caching.md](caching.md) · [Performance/images.md](images.md) · [Performance/rum.md](rum.md) · [Performance/ai-cost.md](ai-cost.md) · [Checklists/performance.md](../Checklists/performance.md)

## AI Instructions

When shipping UI:
1. Set performance budgets upfront. → [Performance/budgets.md](budgets.md)
2. Ship less JS. Question every dependency.
3. Images: AVIF/WebP, `srcset`, `loading="lazy"`, `width`/`height`.
4. Fonts: `font-display: swap`, `preload`, subset.
5. Code-split routes and below-fold components.
6. Use SSR/SSG where appropriate.
7. Add caching headers. → [Performance/caching.md](caching.md)
8. Verify: Lighthouse ≥ 90. LCP < 2.5s, CLS < 0.1, INP < 200ms.

## Human Notes

### Measure first
- **Lab** (Lighthouse, WebPageTest) — synthetic, reproducible.
- **Field** (CrUX, RUM) — real users.

Both matter. Lab catches regressions; field catches reality.

### Targets (mobile)
- LCP < 2.5s
- INP < 200ms
- CLS < 0.1
- TTFB < 800ms
- FCP < 1.8s
- Total JS (gzip) < 150KB

→ [WEB_VITALS.md](../WEB_VITALS.md)

### Top wins (in order)
1. **Images** — compress, modern format, responsive sizes.
2. **JS** — code-split, lazy-load, replace heavy deps.
3. **Caching** — long max-age on static assets, CDN.
4. **Fonts** — `font-display: swap`, `preload`, subset.
5. **HTTP/2+** — multiplexing, header compression.
6. **Preconnect / dns-prefetch** for critical 3rd-party origins.
7. **Critical CSS** — inline above-the-fold CSS.
8. **Tree-shaking** — remove unused exports.
9. **Compression** — Brotli > Gzip.
10. **Server response** — TTFB < 800ms.

→ [PERFORMANCE.md](../PERFORMANCE.md) for more.

### Image optimization
```html
<picture>
  <source type="image/avif" srcset="/img-400.avif 400w, /img-800.avif 800w">
  <source type="image/webp" srcset="/img-400.webp 400w, /img-800.webp 800w">
  <img
    src="/img-800.jpg"
    srcset="/img-400.jpg 400w, /img-800.jpg 800w"
    sizes="(max-width: 600px) 100vw, 50vw"
    alt="..."
    width="800"
    height="600"
    loading="lazy"
    decoding="async"
  >
</picture>
```
→ [Performance/images.md](images.md)

### JS performance
- Code-split routes (Next.js does this automatically).
- Lazy-load below-fold components (`React.lazy` + `Suspense`).
- Replace heavy deps:
  - `moment` → `date-fns` or `dayjs`.
  - `lodash` → native or `radash`.
  - `axios` → `fetch` (modern).
  - `redux` (whole app) → Zustand + TanStack Query.
- Use `requestIdleCallback` for non-critical work.
- Web Workers for heavy compute.

### React performance
- Memoize (sparingly): `useMemo`, `useCallback`, `React.memo`.
- Virtualize long lists (`@tanstack/react-virtual`).
- Avoid inline object/array props (busts memoization).
- Use `key` prop correctly.
- Profile with React DevTools Profiler.

### Network performance
- HTTP/2 or HTTP/3.
- Brotli compression.
- CDN for static assets.
- Preload critical resources.
- `dns-prefetch` / `preconnect` for 3rd-party origins.
- Service Worker for offline caching.

### Caching
- **Browser cache**: `Cache-Control: max-age=...` for static assets.
- **CDN cache**: edge caching.
- **Service Worker**: offline, custom caching strategies.
- **HTTP cache**: stale-while-revalidate.
- **In-memory cache**: for data within session.
- **DB cache**: Redis.

→ [Performance/caching.md](caching.md)

### Render performance
- Avoid layout thrash (batch DOM reads/writes).
- Use `transform`/`opacity` for animations.
- Debounce/throttle expensive handlers.
- `content-visibility: auto` for off-screen content.

### Bundle analysis
```bash
# Vite
npx vite-bundle-visualizer

# Next.js
next build  # see output
ANALYZE=true next build  # with webpack-bundle-analyzer

# Webpack
npx webpack-bundle-analyzer dist/stats.json
```

### RUM (Real User Monitoring)
```js
import { onLCP, onCLS, onINP } from 'web-vitals';

onLCP(metric => sendToAnalytics(metric));
onCLS(metric => sendToAnalytics(metric));
onINP(metric => sendToAnalytics(metric));
```

→ [Performance/rum.md](rum.md)

## Common Mistakes

- ❌ Ship 2MB JS for a content site.
- ❌ Unoptimized images.
- ❌ Render-blocking JS.
- ❌ No caching headers.
- ❌ Fonts causing FOIT/FOUT.
- ❌ Sync third-party scripts.
- ❌ Layout shift from images/ads.
- ❌ Not testing on Slow 3G.

## Tools

- Lighthouse (Chrome DevTools)
- PageSpeed Insights: https://pagespeed.web.dev/
- WebPageTest: https://www.webpagetest.org/
- GTmetrix: https://gtmetrix.com/
- Bundlephobia: https://bundlephobia.com/
- Size Limit: https://github.com/ai/size-limit
- web-vitals: https://github.com/GoogleChrome/web-vitals

## References

- web.dev/performance: https://web.dev/performance
- MDN Performance: https://developer.mozilla.org/en-US/docs/Web/Performance
- Chrome Performance blog: https://developer.chrome.com/blog/

## Further Reading

- *High Performance Browser Networking* — Ilya Grigorik (free)
- *Web Performance in Action* — Jeremy Wagner
- *Image Optimization* — Addy Osmani

## Exercises

1. Audit your site with Lighthouse. Fix top 3 issues.
2. Reduce bundle by 30%.
3. Make your site load <1s on Slow 3G.

## Projects

- Build a RUM dashboard (Postgres + Grafana).
- Set up Lighthouse CI in GitHub Actions.

---

**Previous:** [ThreeJS/](../ThreeJS/) · **Next:** [SEO/](../SEO/) · **Related:** [WEB_VITALS.md](../WEB_VITALS.md)
