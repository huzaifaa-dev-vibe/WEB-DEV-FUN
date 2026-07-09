# SEO (Overview)

> If they can't find you, they can't use you. Deep coverage in [SEO/](SEO/).

---

## Purpose

Make your site discoverable by search engines and humans.

## Prerequisites

- HTML, basic understanding of how search engines work.

## Learning Outcome

You can implement technical SEO, structured data, metadata, sitemaps, and monitor search performance.

## Related Files

- [SEO/](SEO/) — deep dives
- [Performance](PERFORMANCE.md) — perf affects SEO
- [Accessibility](ACCESSIBILITY.md) — a11y helps SEO
- [Checklists/seo.md](Checklists/seo.md)

## AI Instructions

When building a site:
1. Every page has a unique `<title>` (50–60 chars) and `<meta name="description">` (150–160 chars).
2. Use semantic HTML. One `<h1>` per page. Logical heading order.
3. Add OpenGraph (`og:title`, `og:description`, `og:image`, `og:url`) and Twitter Card tags.
4. Add canonical URLs (`<link rel="canonical">`).
5. Generate a sitemap.xml and submit to Google Search Console.
6. Generate robots.txt with appropriate allow/disallow.
7. Add JSON-LD structured data for the content type. → [SEO/schema.md](SEO/schema.md)
8. Ensure mobile-friendly (responsive, no horizontal scroll).
9. Ensure fast load (Core Web Vitals).
10. Use HTTPS, redirect HTTP to HTTPS, no mixed content.

## Human Notes

SEO is three things:
1. **Technical** — can Google crawl and index you?
2. **Content** — does your content match what people search for?
3. **Authority** — do other sites link to you?

This repo covers #1 in depth. #2 and #3 are content/marketing, but they depend on #1 being solid.

## Quick Wins

- Unique title + description per page.
- Semantic HTML.
- Sitemap.xml + robots.txt.
- Submit to Google Search Console + Bing Webmaster Tools.
- OpenGraph tags (for social sharing).
- HTTPS everywhere.
- Mobile-friendly.
- Fast (Core Web Vitals).
- Image `alt` text.
- Internal linking with descriptive anchor text.

## Tools

- **Google Search Console** — https://search.google.com/search-console
- **Bing Webmaster Tools** — https://www.bing.com/webmasters
- **Ahrefs** / **SEMrush** — paid, comprehensive.
- **Screaming Frog** — site crawler (free up to 500 URLs).
- **Schema.org** validator — https://validator.schema.org/
- **Rich Results Test** — https://search.google.com/test/rich-results
- **OpenGraph.xyz** — preview social cards.
- **Lighthouse SEO** — built into Chrome.

## References

- Google Search Central: https://developers.google.com/search
- Google Search blog: https://search.googleblog.com/
- MDN SEO: https://developer.mozilla.org/en-US/docs/Glossary/SEO
- Schema.org: https://schema.org/
- Ahrefs Blog: https://ahrefs.com/blog/
- Backlinko: https://backlinko.com/

## Exercises

1. Audit your site's SEO with Lighthouse. Fix all issues.
2. Add JSON-LD for your content type.
3. Generate a sitemap.xml automatically (Next.js: `app/sitemap.ts`).
4. Test your homepage's social card with OpenGraph.xyz.

## Projects

- Build a blog with perfect SEO (sitemaps, RSS, schema, OG cards).
- Migrate a site from CSR to SSR/SSG and measure SEO impact.

---

**Next:** [SEO/](SEO/) · [WEB_VITALS.md](WEB_VITALS.md) · [Analytics/](Analytics/)
