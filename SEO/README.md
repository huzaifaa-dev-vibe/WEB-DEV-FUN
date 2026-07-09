# SEO

> If they can't find you, they can't use you.

---

## Purpose

Make your site discoverable by search engines and humans.

## Prerequisites

- [HTML/](../HTML/).

## Learning Outcome

You can implement technical SEO, structured data, metadata, sitemaps, and monitor search performance.

## Dependencies

- HTML.

## Related Files

- [SEO.md](../SEO.md) · [Performance/](../Performance/) · [Accessibility/](../Accessibility/) · [Checklists/seo.md](../Checklists/seo.md) · [SEO/schema.md](schema.md)

## AI Instructions

When building a site:
1. Unique `<title>` (50–60 chars) and `<meta name="description">` (150–160) per page.
2. Semantic HTML. One `<h1>` per page.
3. OpenGraph + Twitter Card tags.
4. Canonical URLs.
5. `sitemap.xml` + `robots.txt`.
6. JSON-LD structured data. → [SEO/schema.md](schema.md)
7. Mobile-friendly.
8. Fast (Core Web Vitals).
9. HTTPS, no mixed content.
10. Internal links with descriptive anchor text.

## Human Notes

SEO = Technical + Content + Authority.

### Technical SEO checklist
- [ ] Unique title per page.
- [ ] Unique meta description per page.
- [ ] Semantic HTML.
- [ ] One `<h1>` per page.
- [ ] Logical heading order.
- [ ] All images have `alt`.
- [ ] Mobile-friendly (responsive).
- [ ] HTTPS.
- [ ] Sitemap.xml.
- [ ] Robots.txt.
- [ ] Canonical URLs.
- [ ] OpenGraph + Twitter Card.
- [ ] JSON-LD schema.
- [ ] Fast (Core Web Vitals).
- [ ] No broken links.
- [ ] 301 redirects for moved pages.
- [ ] 404 page exists.
- [ ] Breadcrumb navigation.
- [ ] XML sitemap submitted to Search Console.
- [ ] No duplicate content.
- [ ] No cloaking.
- [ ] hreflang for multi-language.

### Metadata
```html
<head>
  <title>Page Title | Site Name</title>
  <meta name="description" content="Page description for SEO.">
  <link rel="canonical" href="https://example.com/page">

  <!-- OpenGraph -->
  <meta property="og:title" content="Page Title">
  <meta property="og:description" content="Page description.">
  <meta property="og:image" content="https://example.com/og.png">
  <meta property="og:url" content="https://example.com/page">
  <meta property="og:type" content="website">

  <!-- Twitter -->
  <meta name="twitter:card" content="summary_large_image">
  <meta name="twitter:title" content="Page Title">
  <meta name="twitter:description" content="Page description.">
  <meta name="twitter:image" content="https://example.com/twitter.png">
</head>
```

### Sitemap
```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://example.com/</loc>
    <lastmod>2025-01-15</lastmod>
    <changefreq>daily</changefreq>
    <priority>1.0</priority>
  </url>
</urlset>
```

Next.js: `app/sitemap.ts`. Astro: integration. Most frameworks handle this.

### Robots.txt
```
User-agent: *
Allow: /
Disallow: /admin/
Sitemap: https://example.com/sitemap.xml
```

### Structured data (JSON-LD)
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "Article Title",
  "author": { "@type": "Person", "name": "Author Name" },
  "datePublished": "2025-01-15",
  "image": "https://example.com/image.jpg"
}
</script>
```

→ [SEO/schema.md](schema.md) for all types.

### Content SEO
- Match search intent.
- Use keywords naturally (no stuffing).
- Long-form tends to rank (when comprehensive).
- Update old content.
- Internal linking.

### Authority (off-page)
- Backlinks from authoritative sites.
- Brand mentions.
- Social signals (debated).
- Fresh, shareable content.

### Common SEO issues
- Thin content.
- Duplicate content.
- Slow load.
- Mobile-unfriendly.
- Broken links.
- Missing canonical.
- Wrong hreflang.
- Blocked in robots.txt.
- Noindex by accident.
- No sitemap.

## Tools

- Google Search Console: https://search.google.com/search-console
- Bing Webmaster Tools: https://www.bing.com/webmasters
- Ahrefs: https://ahrefs.com/
- SEMrush: https://www.semrush.com/
- Screaming Frog: https://www.screamingfrog.com/
- Schema validator: https://validator.schema.org/
- Rich Results Test: https://search.google.com/test/rich-results
- OpenGraph.xyz: https://opengraph.xyz/
- Lighthouse SEO.

## References

- Google Search Central: https://developers.google.com/search
- Google Search blog: https://search.googleblog.com/
- MDN SEO: https://developer.mozilla.org/en-US/docs/Glossary/SEO
- Schema.org: https://schema.org/
- Ahrefs Blog: https://ahrefs.com/blog/
- Backlinko: https://backlinko.com/

## Further Reading

- *SEO for Growth* — John Jantsch
- *The Art of SEO* — Eric Enge

## Exercises

1. Audit your site's SEO with Lighthouse. Fix all issues.
2. Add JSON-LD for your content type.
3. Generate a sitemap.xml automatically.
4. Test your social card with OpenGraph.xyz.

## Projects

- Build a blog with perfect SEO (sitemaps, RSS, schema, OG cards).
- Migrate a CSR site to SSR/SSG. Measure SEO impact.

---

**Previous:** [Performance/](../Performance/) · **Next:** [Analytics/](../Analytics/) · **Related:** [WEB_VITALS.md](../WEB_VITALS.md)
