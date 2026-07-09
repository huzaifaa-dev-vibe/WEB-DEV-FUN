# Project: Personal Portfolio

> Beginner-friendly portfolio site. Ship in a weekend.

---

## Goal

Build a personal portfolio that showcases your work, gets you hired, and doesn't look like every other portfolio.

## Users / Personas
- **Recruiters** — scanning for "can this person do the job?"
- **Engineering managers** — looking for proof of work.
- **Fellow developers** — looking for inspiration / collaboration.

## Features (MVP)
- Hero with name + one-line pitch.
- About section (2-3 sentences, not a novel).
- Projects (3-6, real, with links).
- Contact (email + socials).
- Dark mode.
- Responsive.
- Accessible.
- SEO basics (sitemap, OG cards, meta).

## Features (v2)
- Blog.
- Speaking / talks.
- Now page.
- Uses page.
- Stats (GitHub, WakaTime).
- Newsletter.

## Architecture
```
app/
  layout.tsx
  page.tsx                 # hero
  about/page.tsx
  projects/page.tsx
  projects/[slug]/page.tsx # project detail
  contact/page.tsx
  rss.xml
  sitemap.ts
  robots.ts
components/
  Hero.tsx
  ProjectCard.tsx
  Nav.tsx
  Footer.tsx
content/
  projects/*.mdx
lib/
  projects.ts
public/
  og.png
```

## Tech Stack (verified)
- Next.js 15 (App Router).
- TypeScript (strict).
- Tailwind CSS 4.
- shadcn/ui (optional).
- MDX for project content.
- Vercel for deploy.

## AI Prompt

```
You are a senior frontend engineer.

Build a personal portfolio for "<NAME>", a "<ROLE>".

Read these files first:
- /AI_AGENT_GUIDE.md
- /ANTI-AI-DESIGN/README.md
- /ANTI-AI-DESIGN/hero-alternatives.md
- /Website-Blueprints/portfolio.md

Requirements:
- Next.js 15 App Router + TypeScript strict + Tailwind.
- Hero: NOT centered + 2 CTAs. Pick an alternative from /ANTI-AI-DESIGN/hero-alternatives.md.
- About: 3 sentences max.
- Projects: 3-6 real projects, with links, screenshots.
- Contact: email + socials.
- Dark mode (real, not just inverted).
- Responsive (375px mobile, 1440px desktop).
- Accessible (keyboard, contrast, focus-visible).
- SEO (sitemap.xml, robots.txt, OG cards, meta).
- No emoji icons. Use Lucide.
- No purple-pink gradient.
- One intentional imperfection.

Output:
- Full Next.js project.
- README with how to run.
```

## Challenges
- Don't look like every other portfolio.
- Don't fake projects. Use real ones (or build them).
- Don't write a long bio. Recruiters don't read.

## Extensions
- Add a blog (MDX).
- Add a "Now" page.
- Add GitHub stats.
- Add a newsletter signup.

## Checklist

→ [Checklists/pre-launch.md](../Checklists/pre-launch.md)

Highlights:
- [ ] Lighthouse mobile ≥ 90.
- [ ] LCP < 2.5s.
- [ ] axe 0 issues.
- [ ] Real OG card.
- [ ] Real favicon.
- [ ] Sitemap submitted.
- [ ] Deploy to Vercel.
- [ ] Custom domain.

## Inspiration
- https://github.com/anthonyshort/awesome-portfolios
- https://godly.website/category/portfolio
- https://www.nngroup.com/articles/portfolio-personal-site/

---

**Next:** [blog.md](blog.md) · Back to [Projects/](README.md)
