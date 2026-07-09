# Performance Checklist

> Run on every UI change.

## Web Vitals
- [ ] LCP < 2.5s (mobile).
- [ ] CLS < 0.1.
- [ ] INP < 200ms.
- [ ] TTFB < 800ms.
- [ ] FCP < 1.8s.

## Bundle
- [ ] Total JS (gzip) < 150KB on first load.
- [ ] Total CSS < 30KB.
- [ ] No single chunk > 100KB.
- [ ] Tree-shaking working.
- [ ] Code-split routes.
- [ ] Lazy-load below-fold components.
- [ ] No unused exports in bundle.

## Images
- [ ] AVIF/WebP for all images.
- [ ] `srcset` for responsive sizes.
- [ ] `loading="lazy"` on below-fold.
- [ ] `width` and `height` on all images.
- [ ] `fetchpriority="high"` on LCP image.
- [ ] Compressed (Squoosh / ImageOptim).
- [ ] SVGs optimized (SVGO).

## Fonts
- [ ] Self-hosted (Fontsource) or privacy-friendly CDN.
- [ ] `font-display: swap`.
- [ ] `preload` critical font.
- [ ] Subset to languages used.
- [ ] Variable fonts where possible.
- [ ] Max 2 fonts.

## Network
- [ ] HTTP/2 or HTTP/3.
- [ ] Brotli compression.
- [ ] CDN for static assets.
- [ ] Long `Cache-Control` for static.
- [ ] `preconnect` to critical 3rd-party origins.
- [ ] `dns-prefetch` for likely 3rd-party.
- [ ] No render-blocking JS in `<head>`.
- [ ] Critical CSS inlined.

## JavaScript
- [ ] No `setTimeout` for async flow.
- [ ] Debounce/throttle expensive handlers.
- [ ] Web Workers for heavy compute.
- [ ] `requestIdleCallback` for non-critical.
- [ ] Memoize where it matters (don't over-memoize).
- [ ] Virtualize long lists.
- [ ] No layout thrash.

## React-specific
- [ ] Server Components by default.
- [ ] `'use client'` only where needed.
- [ ] `key` prop on lists (stable, unique).
- [ ] No inline object/array props (busts memo).
- [ ] Profile with React DevTools.

## Database
- [ ] No N+1 queries.
- [ ] Indexes on FKs + frequent WHERE.
- [ ] `EXPLAIN ANALYZE` on slow queries.
- [ ] Connection pooling.
- [ ] Cursor pagination (not offset).

## Caching
- [ ] HTTP cache headers set.
- [ ] CDN cache configured.
- [ ] In-app cache (Redis) where appropriate.
- [ ] Service Worker for offline (PWA).

## Server
- [ ] TTFB < 800ms.
- [ ] Edge rendering where possible.
- [ ] Streaming responses.
- [ ] Timeouts on all external calls.

## Third-Party
- [ ] Audit all 3rd-party scripts.
- [ ] Load 3rd-party async/defer.
- [ ] Use Partytown for non-critical.
- [ ] Remove unused.

## Measurement
- [ ] Lighthouse CI in CI/CD.
- [ ] RUM (real-user monitoring) installed.
- [ ] Performance budget enforced.
- [ ] Alert on regression.

---

**Next:** [security.md](security.md) · Back to [Checklists/](README.md)
