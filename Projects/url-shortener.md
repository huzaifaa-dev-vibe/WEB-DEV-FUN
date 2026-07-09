# Project: URL Shortener

> A classic systems-design project. Scales to billions of URLs.

---

## Goal

Build a URL shortener that's fast, scalable, and production-grade.

## Users
- **End users** — shorten URLs, click them.
- **Admins** — see analytics, manage abuse.

## Features (MVP)
- Shorten URL → return short URL.
- Redirect short URL → original.
- Click analytics (count, referrer, country).
- Custom slugs (optional).
- Expiration (optional).

## Features (v2)
- User accounts.
- Custom domains.
- QR codes.
- Bulk import.
- API.
- Rate limiting per IP / per user.
- Spam detection.

## Architecture

```
[Browser] → [CDN/Edge] → [API] → [Cache (Redis)] → [DB (Postgres)]
```

- Short URL: 7-char base62 code.
- Cache: Redis (cache-aside).
- DB: Postgres (id, original_url, short_code, created_at, expires_at, user_id).
- Click tracking: insert into `clicks` table (or async via queue).

## Folder Structure
```
app/
  [code]/route.ts          # redirect
  api/
    shorten/route.ts
    urls/route.ts          # list user's URLs
    urls/[id]/route.ts     # CRUD
  page.tsx                 # homepage with shorten form
  dashboard/page.tsx
components/
  ShortenForm.tsx
  UrlTable.tsx
lib/
  db.ts
  shortener.ts             # base62 encode
  cache.ts
```

## Data Model
```sql
CREATE TABLE urls (
  id BIGSERIAL PRIMARY KEY,
  original_url TEXT NOT NULL,
  short_code VARCHAR(7) NOT NULL UNIQUE,
  user_id BIGINT REFERENCES users(id),
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  expires_at TIMESTAMPTZ,
  click_count BIGINT NOT NULL DEFAULT 0
);

CREATE INDEX idx_urls_short_code ON urls (short_code);

CREATE TABLE clicks (
  id BIGSERIAL PRIMARY KEY,
  url_id BIGINT NOT NULL REFERENCES urls(id) ON DELETE CASCADE,
  clicked_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  referrer TEXT,
  country VARCHAR(2),
  user_agent TEXT
);

CREATE INDEX idx_clicks_url_id ON clicks (url_id);
```

For scale: time-partition `clicks` by day/week.

## Tech Stack (verified)
- Next.js 15 (App Router).
- Postgres 16 (Neon / Supabase for serverless).
- Redis 7 (Upstash for serverless).
- TypeScript strict.
- Tailwind.
- Vercel for deploy.

## Short Code Algorithm

Option 1: Convert auto-increment ID to base62.
```ts
const BASE62 = '0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz';
function encode(n: number): string {
  if (n === 0) return BASE62[0];
  let s = '';
  while (n > 0) {
    s = BASE62[n % 62] + s;
    n = Math.floor(n / 62);
  }
  return s.padStart(7, '0');
}
```

Option 2: Random 7-char string (check collision).

Option 3: Hash(original_url + timestamp) → first 7 chars.

For scale: option 1 with a "counter" service (Redis INCR).

## AI Prompt

```
Build a URL shortener per /Projects/url-shortener.md.

Read first:
- /AI_AGENT_GUIDE.md
- /Projects/url-shortener.md
- /REST/README.md
- /Performance/caching.md

Stack: Next.js 15 + Postgres + Redis + TypeScript strict.

Endpoints:
- POST /api/shorten { url } → { short_url }
- GET /:code → 301 redirect to original (or 404)
- GET /api/urls → list user's URLs
- GET /api/urls/:id/stats → click stats

Implement:
- Cache-aside with Redis.
- Rate limiting per IP.
- Click tracking (async via queue).
- Custom slugs (optional).
- Expiration.

Run /Checklists/pre-launch.md before reporting done.
```

## Challenges
- **Cache invalidation** — when URL deleted, evict from cache.
- **Click tracking at scale** — async queue, batch insert.
- **Spam** — rate limit, blacklist, manual review.
- **Custom slugs** — collision detection.

## Extensions
- User accounts + auth.
- Custom domains (CNAME to your service).
- QR codes (generate via API).
- Bulk import (CSV).
- API with tokens.
- Analytics dashboard.

## Checklist
- [ ] LCP < 1s (it's a simple page).
- [ ] Cache hit rate > 90%.
- [ ] Redirect < 100ms p99.
- [ ] Rate limiting works.
- [ ] Click tracking accurate.
- [ ] 0 security holes.

## References
- ByteByteGo URL shortener: https://bytebytego.com/articles/design-a-url-shortener
- System Design Primer: https://github.com/donnemartin/system-design-primer

---

**Next:** [chat-app.md](chat-app.md) · Back to [Projects/](README.md)
