# Anti-AI-Design: Principles

> The 10 principles that make UI look human-designed.

---

## 1. Intention over convention

Every choice — color, spacing, type, layout — has a reason that you can articulate. If your only reason is "that's how it's done", reconsider.

**AI tell:** Default Tailwind classes, default shadcn components with no customization, default Next.js starter layout.

**Human alternative:** Customize tokens. Pick a hero layout that fits the content. Have opinions about whitespace.

---

## 2. Asymmetry creates hierarchy

Not everything should be centered. Not everything should be aligned to a grid. Asymmetry draws the eye and creates visual interest.

**AI tell:** Centered hero. Centered section titles. Centered cards.

**Human alternative:** Asymmetric hero (text left, image right, or vice versa). Off-center section titles. Numbered list aligned left.

---

## 3. Constraint creates voice

Limit your palette, your typefaces, your radii. The constraints become your voice.

**AI tell:** 7 colors, 4 fonts, 3 radius sizes — all used randomly.

**Human alternative:** 1 accent color, 1 typeface (with weight contrast), 2-3 radii used consistently by purpose (small for inputs, medium for cards, full for pills).

---

## 4. Real copy beats placeholder

Lorem ipsum is the loudest AI tell. Generic copy ("We provide innovative solutions") is the second loudest.

**AI tell:** "Lorem ipsum dolor sit amet" or "Lorem" in a hero. "We are a team of passionate innovators."

**Human alternative:** Real copy. Even if rough. Write the headline you'd actually want. → [copywriting.md](copywriting.md)

---

## 5. Real photos beat stock

Stock photos of "diverse team laughing at laptop" are instantly recognizable. So is Unsplash-photo-of-mountains.

**AI tell:** Unsplash random photo. "Business team meeting" stock.

**Human alternative:**
- Real product screenshots.
- Real photos of your team / office / product.
- Custom illustrations (even simple).
- No photos at all (use typography, color, layout).

→ [photography.md](photography.md)

---

## 6. One typeface, used well, beats five

Most great designs use one typeface with weight/size contrast. Sometimes two (sans + serif).

**AI tell:** 4 different Google Fonts. Display font + body font + accent font + mono. All mixed.

**Human alternative:** One typeface (Inter, Geist, etc.) with 3 weights (400, 500, 700). Maybe one display face for hero only.

→ [typography.md](typography.md)

---

## 7. Motion explains state

Animation should explain a state change (modal opening, list reordering, item added). Not decorate (parallax for its own sake, fade-in-up on every section).

**AI tell:** `fade-in-up` on every section. Floating animations on cards. Auto-rotating carousels.

**Human alternative:** Animate modal open/close. Animate list reordering (Framer Motion `layout`). Subtle hover states. Respect `prefers-reduced-motion`.

→ [motion.md](motion.md)

---

## 8. Imperfection is human

Slight rotation. Hand-drawn elements. Asymmetric grids. Off-grid elements. Perfect symmetry is the AI tell.

**AI tell:** Perfectly aligned grid. Every card same size. Every gap same.

**Human alternative:** Slight rotation on hero image. Hand-drawn underline. Masonry layout for gallery. Mixed card sizes (feature card 2x bigger than others).

→ [imperfections.md](imperfections.md)

---

## 9. Density varies

Not every section should breathe the same. Some should be dense (dashboard, list). Some should breathe (hero, quote).

**AI tell:** Every section has `py-24`. Every card has `p-8`. Every gap is `gap-6`.

**Human alternative:** Hero has more space (py-32). Feature grid is tighter (py-16). Footer is dense (py-12).

→ [spacing.md](spacing.md)

---

## 10. Voice is consistent

Pick a tone (formal, casual, technical, playful) and stay. Don't be playful in the hero and formal in the docs.

**AI tell:** Hero says "Build amazing things 🚀". Docs say "The system facilitates the deployment of..."

**Human alternative:** Consistent voice across the site. Pick "casual technical" and apply everywhere: "Ship things faster. Here's how."

→ [copywriting.md](copywriting.md)

---

## How to apply

Read these principles once. Print them. Tape them next to your monitor. Re-read before every UI task.

When reviewing your work, ask: "Would a senior designer call this AI-generated?" If yes, fix it.

→ [checklist.md](checklist.md)

---

**Next:** [hero-alternatives.md](hero-alternatives.md) · [checklist.md](checklist.md) · Back to [ANTI-AI-DESIGN/](README.md)
