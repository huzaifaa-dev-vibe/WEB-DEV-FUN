# EXTERNAL REPOSITORIES

> The best of the OSS web ecosystem, organized by topic. Every entry: what it is, why use it, popularity, when to use, alternatives.

This file is the curated catalog. It's how you pick the right tool without guessing.

**For AI agents:** Before importing ANY package, find it here (or add it here). Verify it exists at the version you're using. Don't hallucinate package names.

---

## How to Read Entries

```
### Package Name
- **Repo:** link
- **Stars:** approximate (at time of writing — verify)
- **What:** one sentence
- **Why:** when to use
- **When not:** when NOT to use
- **Alternatives:** other options
```

---

## Frontend Frameworks

### React
- **Repo:** https://github.com/facebook/react
- **Stars:** 230K+
- **What:** Component-based UI library.
- **Why:** Industry default. Huge ecosystem. Jobs.
- **When not:** Static content sites (use Astro). Tiny apps (use Svelte/Vue).
- **Alternatives:** Vue, Svelte, Solid, Angular, Qwik.

### Vue
- **Repo:** https://github.com/vuejs/core
- **Stars:** 45K+
- **What:** Progressive framework.
- **Why:** Approachable. Single-file components. Great docs.
- **When not:** You need React's ecosystem.
- **Alternatives:** React, Svelte, Solid.

### Svelte / SvelteKit
- **Repo:** https://github.com/sveltejs/svelte
- **Stars:** 80K+
- **What:** Compiler-based framework. No virtual DOM.
- **Why:** Smallest bundles. Best DX for many. SvelteKit is a great meta-framework.
- **When not:** Largest ecosystem needed.
- **Alternatives:** React, Vue, Solid, Astro.

### Angular
- **Repo:** https://github.com/angular/angular
- **Stars:** 95K+
- **What:** Batteries-included framework.
- **Why:** Enterprise default. Opinions. TypeScript-first.
- **When not:** Small teams. Lightweight apps.
- **Alternatives:** React, Vue.

### Solid
- **Repo:** https://github.com/solidjs/solid
- **Stars:** 32K+
- **What:** React-like syntax, no VDOM, fine-grained reactivity.
- **Why:** Fastest React-like.
- **When not:** Ecosystem smaller than React.
- **Alternatives:** React, Svelte, Qwik.

### Qwik
- **Repo:** https://github.com/BuilderIO/qwik
- **Stars:** 21K+
- **What:** Resumable framework. Zero JS until interaction.
- **Why:** Best first-load performance for apps.
- **When not:** Ecosystem young. Team unfamiliar.
- **Alternatives:** Astro (for content), Solid, React.

### Preact
- **Repo:** https://github.com/preactjs/preact
- **Stars:** 36K+
- **What:** 3KB React alternative.
- **Why:** Tiny bundles.
- **When not:** Need full React compatibility (some libraries don't work).
- **Alternatives:** React, Solid.

---

## Meta-Frameworks

### Next.js
- **Repo:** https://github.com/vercel/next.js
- **Stars:** 125K+
- **What:** React meta-framework. App Router, RSC, SSR/SSG/ISR.
- **Why:** Default for React. Vercel deployment. AI SDK.
- **When not:** Pure content site (use Astro). Heavy backend (use a backend framework).
- **Alternatives:** Remix (now React Router), TanStack Start, Astro, SvelteKit.

### React Router (v7, formerly Remix)
- **Repo:** https://github.com/remix-run/react-router
- **Stars:** 53K+
- **What:** Web standards-based React framework.
- **Why:** Better data loading patterns than Next for some cases. Web standards.
- **When not:** Already deep in Next ecosystem.
- **Alternatives:** Next.js, TanStack Start.

### TanStack Start
- **Repo:** https://github.com/TanStack/router
- **Stars:** 8K+
- **What:** Type-safe React framework built on TanStack Router.
- **Why:** Type safety. Built by the TanStack team.
- **When not:** Ecosystem young.
- **Alternatives:** Next.js, Remix.

### Nuxt
- **Repo:** https://github.com/nuxt/nuxt
- **Stars:** 53K+
- **What:** Vue meta-framework.
- **Why:** Vue equivalent of Next.
- **Alternatives:** Next.js, SvelteKit, Astro.

### SvelteKit
- **Repo:** https://github.com/sveltejs/kit
- **Stars:** 18K+
- **What:** Svelte meta-framework.
- **Why:** Best DX for Svelte apps.
- **Alternatives:** Next.js, Nuxt, Astro.

### Astro
- **Repo:** https://github.com/withastro/astro
- **Stars:** 45K+
- **What:** Content-first framework. Islands architecture.
- **Why:** Best for blogs, docs, marketing sites. Zero JS by default.
- **When not:** App-like interactivity throughout.
- **Alternatives:** Next.js (with SSG), Eleventy, Hugo.

### Remix (now merged into React Router v7)
- See React Router above.

### Angular Universal / Analog
- **Repo:** https://github.com/analogjs/analog
- **What:** Meta-framework for Angular.
- **Alternatives:** Next.js (if React ok).

---

## Build Tools & Bundlers

### Vite
- **Repo:** https://github.com/vitejs/vite
- **Stars:** 65K+
- **What:** Next-gen build tool. Dev server + bundler.
- **Why:** Default for new SPAs. Fast HMR. Powered by esbuild + Rollup.
- **Alternatives:** Turbopack (Next), Webpack (legacy), Rspack.

### Turbopack
- **Repo:** https://github.com/vercel/turbo
- **Stars:** 26K+
- **What:** Rust-based bundler from Vercel. Replaces Webpack in Next.
- **Why:** Speed. Built into Next.js.
- **When not:** Mature ecosystem? Webpack plugins you depend on.

### Rspack
- **Repo:** https://github.com/web-infra-dev/rspack
- **Stars:** 10K+
- **What:** Rust-based Webpack-compatible bundler.
- **Why:** Drop-in Webpack replacement, 10x faster.
- **Alternatives:** Vite, esbuild.

### esbuild
- **Repo:** https://github.com/evanw/esbuild
- **Stars:** 38K+
- **What:** Go-based JS bundler. Very fast.
- **Why:** Powering Vite's dev server. Library builds.
- **When not:** Need advanced bundling features.

### Rollup
- **Repo:** https://github.com/rollup/rollup
- **Stars:** 25K+
- **What:** ES module bundler.
- **Why:** Library builds. Tree-shaking.
- **Alternatives:** esbuild, tsup.

### tsup
- **Repo:** https://github.com/egoist/tsup
- **Stars:** 9K+
- **What:** Zero-config TS bundler built on esbuild.
- **Why:** Easiest way to ship a TS library.
- **Alternatives:** Rollup, Microbundle.

### SWC
- **Repo:** https://github.com/swc-project/swc
- **Stars:** 30K+
- **What:** Rust-based JS/TS compiler.
- **Why:** Powers Next.js, Turbopack, Deno.

### Bun
- See [Bun/](Bun/). Also a bundler.

### Parcel
- **Repo:** https://github.com/parcel-bundler/parcel
- **Stars:** 43K+
- **What:** Zero-config bundler.
- **Why:** Truly zero-config.
- **When not:** Vite is faster and more popular now.

---

## CSS Tools & Frameworks

### Tailwind CSS
- **Repo:** https://github.com/tailwindlabs/tailwindcss
- **Stars:** 80K+
- **What:** Utility-first CSS framework.
- **Why:** Default for new projects. v4 is even faster.
- **When not:** Team strongly prefers CSS-in-JS or scoped CSS.
- **Alternatives:** UnoCSS, Panda CSS, vanilla-extract.

### UnoCSS
- **Repo:** https://github.com/unocss/unocss
- **Stars:** 16K+
- **What:** Atomic CSS engine, faster than Tailwind.
- **Why:** Customizable. Faster.
- **When not:** Want Tailwind's defaults out of the box.

### Panda CSS
- **Repo:** https://github.com/chakra-ui/panda
- **Stars:** 6K+
- **What:** CSS-in-JS at build time.
- **Why:** Type-safe. Build-time extracted.
- **Alternatives:** vanilla-extract, Stitches.

### vanilla-extract
- **Repo:** https://github.com/vanilla-extract-css/vanilla-extract
- **Stars:** 10K+
- **What:** Zero-runtime CSS-in-TS.
- **Why:** Type-safe CSS without runtime cost.
- **Alternatives:** Panda CSS, CSS Modules.

### CSS Modules
- Built into most bundlers.
- **Why:** Scoped CSS without deps.

### Stitches
- **Repo:** https://github.com/stitchesjs/stitches
- **Status:** Maintenance mode. Use Panda instead.

### Emotion
- **Repo:** https://github.com/emotion-js/emotion
- **Stars:** 17K+
- **What:** Runtime CSS-in-JS.
- **When not:** Performance-critical (prefer build-time solutions).

### styled-components
- **Repo:** https://github.com/styled-components/styled-components
- **Stars:** 40K+
- **What:** Original CSS-in-JS.
- **When not:** New projects (use Tailwind or vanilla-extract).

### PostCSS
- **Repo:** https://github.com/postcss/postcss
- **Stars:** 28K+
- **What:** CSS transformer. Plugin ecosystem.
- **Why:** Powers Tailwind, Autoprefixer, etc.

### Lightning CSS
- **Repo:** https://github.com/parcel-bundler/lightningcss
- **Stars:** 6K+
- **What:** Rust-based CSS parser/transformer.
- **Why:** 100x faster than PostCSS for many ops.

### Open Props
- **Repo:** https://github.com/argyleink/open-props
- **Stars:** 4K+
- **What:** CSS variables for design tokens.
- **Why:** Drop-in design tokens.

---

## Component Libraries

### shadcn/ui
- **Repo:** https://github.com/shadcn-ui/ui
- **Stars:** 65K+
- **What:** Copy-paste components built on Radix + Tailwind.
- **Why:** You own the code. No library lock-in. Beautiful defaults.
- **When not:** Want a managed library (use Mantine).
- **Alternatives:** Mantine, Radix (the primitives), Park UI.

### Radix UI
- **Repo:** https://github.com/radix-ui/primitives
- **Stars:** 16K+
- **What:** Unstyled, accessible primitives.
- **Why:** Build your own component library on top.
- **Alternatives:** Headless UI, React Aria.

### Headless UI
- **Repo:** https://github.com/tailwindlabs/headlessui
- **Stars:** 26K+
- **What:** Unstyled accessible components from Tailwind team.
- **Why:** Pairs well with Tailwind.

### React Aria / React Aria Components
- **Repo:** https://github.com/adobe/react-spectrum
- **Stars:** 12K+
- **What:** Adobe's accessible hooks + components.
- **Why:** Best-in-class accessibility.

### Mantine
- **Repo:** https://github.com/mantinedev/mantine
- **Stars:** 26K+
- **What:** Full-featured React component library.
- **Why:** Managed, batteries-included. Hooks library too.
- **Alternatives:** Chakra UI, MUI.

### Chakra UI
- **Repo:** https://github.com/chakra-ui/chakra-ui
- **Stars:** 38K+
- **What:** Simple, modular, accessible component library.
- **Why:** Easy to learn.
- **When not:** v3 changed a lot; check status before adopting.

### Material UI (MUI)
- **Repo:** https://github.com/mui/material-ui
- **Stars:** 92K+
- **What:** Material Design components.
- **Why:** Comprehensive. Mature.
- **When not:** Don't want Material look.

### Ant Design
- **Repo:** https://github.com/ant-design/ant-design
- **Stars:** 91K+
- **What:** Enterprise UI library (Chinese origin).
- **Why:** Comprehensive for admin/dashboard UIs.
- **When not:** Non-Chinese B2C (style may feel heavy).

### Park UI
- **Repo:** https://github.com/cschroeter/park-ui
- **Stars:** 1K+
- **What:** Multi-framework components on Ark UI.

### Ark UI
- **Repo:** https://github.com/chakra-ui/ark-ui
- **Stars:** 3K+
- **What:** Headless components for React, Vue, Solid.

### DaisyUI
- **Repo:** https://github.com/saadeghi/daisyui
- **Stars:** 33K+
- **What:** Tailwind component classes.
- **Why:** Quick themes on top of Tailwind.

### Aceternity UI
- **Repo:** https://github.com/aceternity/aceternity-ui
- **What:** Animated, modern components. Trendy.
- **Why:** Visual flair for landing pages.

### Magic UI
- **Repo:** https://github.com/magicuidesign/magicui
- **Stars:** 16K+
- **What:** Animated React components.

### Origin UI
- **Repo:** https://github.com/origin-space/originui
- **What:** Beautifully designed components.

### HyperUI
- **Repo:** https://github.com/markmead/hyperui
- **Stars:** 11K+
- **What:** Tailwind CSS components.

### Flowbite
- **Repo:** https://github.com/themesberg/flowbite
- **Stars:** 7K+
- **What:** Tailwind component library.

### NextUI (now HeroUI)
- **Repo:** https://github.com/heroui-inc/heroui
- **Stars:** 21K+
- **What:** Modern, animated React UI library.

### Tremor
- **Repo:** https://github.com/tremorlabs/tremor
- **Stars:** 15K+
- **What:** React components for dashboards.

### shadcn/ui-inspired for Vue: shadcn-vue
- **Repo:** https://github.com/radix-vue/shadcn-vue

### Reka UI (Vue Radix)
- **Repo:** https://github.com/unovue/reka-ui
- **What:** Vue port of Radix.

---

## Forms & Validation

### React Hook Form
- **Repo:** https://github.com/react-hook-form/react-hook-form
- **Stars:** 40K+
- **What:** Performant form library.
- **Why:** Default for React. Minimal re-renders.

### TanStack Form
- **Repo:** https://github.com/TanStack/form
- **Stars:** 3K+
- **What:** Framework-agnostic form library.
- **Why:** Type-safe. Agnostic.

### Formik
- **Repo:** https://github.com/jaredpalmer/formik
- **Stars:** 34K+
- **What:** Older React form library.
- **When not:** Use React Hook Form for new projects.

### Zod
- **Repo:** https://github.com/colinhacks/zod
- **Stars:** 35K+
- **What:** TypeScript-first schema validation.
- **Why:** Default for runtime validation. Pairs with RHF, tRPC, Next.js.
- **Alternatives:** Valibot (smaller), Yup (older).

### Valibot
- **Repo:** https://github.com/fabian-hiller/valibot
- **Stars:** 6K+
- **What:** Smaller alternative to Zod.
- **Why:** Tree-shakeable. ~700 bytes for basic schemas.

### Yup
- **Repo:** https://github.com/jquense/yup
- **Stars:** 23K+
- **What:** Schema validator. Older.
- **When not:** Use Zod for TS.

### Superforms
- **Repo:** https://github.com/ciscoheat/superforms
- **Stars:** 2K+
- **What:** SvelteKit form library.

### Conform
- **Repo:** https://github.com/edmundhung/conform
- **Stars:** 2K+
- **What:** Progressive enhancement form library for React.

---

## State Management

### Zustand
- **Repo:** https://github.com/pmndrs/zustand
- **Stars:** 45K+
- **What:** Small, fast, hook-based state.
- **Why:** Default for client state.

### Jotai
- **Repo:** https://github.com/pmndrs/jotai
- **Stars:** 18K+
- **What:** Atomic state management.
- **Why:** Bottom-up state.

### TanStack Query (React Query)
- **Repo:** https://github.com/TanStack/query
- **Stars:** 41K+
- **What:** Server state management.
- **Why:** Default for data fetching + caching.

### Redux Toolkit
- **Repo:** https://github.com/reduxjs/redux-toolkit
- **Stars:** 10K+
- **What:** Official Redux toolset.
- **When not:** For new small apps, Zustand + TanStack Query is simpler.

### MobX
- **Repo:** https://github.com/mobxjs/mobx
- **Stars:** 27K+
- **What:** Observable state.
- **When not:** Redux-style is preferred by team.

### Pinia
- **Repo:** https://github.com/vuejs/pinia
- **Stars:** 12K+
- **What:** Vue's official state.
- **Why:** Default for Vue.

### Svelte stores
- Built into Svelte.

### XState
- **Repo:** https://github.com/statelyai/xstate
- **Stars:** 27K+
- **What:** State machines.
- **Why:** Complex flows. Visual editor (Stately).

---

## Data Fetching & RPC

### TanStack Query
- See above.

### SWR
- **Repo:** https://github.com/vercel/swr
- **Stars:** 30K+
- **What:** React data fetching. Vercel's alternative to TanStack Query.

### tRPC
- **Repo:** https://github.com/trpc/trpc
- **Stars:** 35K+
- **What:** End-to-end typesafe APIs without schemas.
- **Why:** Best DX for full-stack TS monorepos.
- **When not:** Public API for external consumers (use REST/GraphQL).

### Relay
- **Repo:** https://github.com/facebook/relay
- **Stars:** 18K+
- **What:** GraphQL client from Meta.
- **When not:** Steep learning curve; Apollo easier.

### Apollo Client
- **Repo:** https://github.com/apollographql/apollo-client
- **Stars:** 19K+
- **What:** GraphQL client.

### urql
- **Repo:** https://github.com/urigo/urql
- **Stars:** 8K+
- **What:** Lightweight GraphQL client.

---

## Routing (Client)

### React Router
- See above (now includes Remix features).

### TanStack Router
- **Repo:** https://github.com/TanStack/router
- **Stars:** 8K+
- **What:** Type-safe router for React.
- **Why:** Best type safety.

### Vue Router
- Built into Vue.

### @tanstack/solid-router / solid-router
- For Solid.

---

## Animations

### Framer Motion (now "Motion")
- **Repo:** https://github.com/framer/motion
- **Stars:** 23K+
- **What:** React animation library.
- **Why:** Best DX for declarative animations.

### Motion One
- **Repo:** https://github.com/motiondivision/motionone
- **What:** Web Animations API wrapper, tiny.

### GSAP
- **Repo:** https://github.com/greensock/GSAP
- **Stars:** 20K+
- **What:** Industry-standard animation engine.
- **Why:** ScrollTrigger, complex timelines.

### Lottie
- **Repo:** https://github.com/airbnb/lottie-web
- **Stars:** 28K+
- **What:** After Effects → web animations.

### Auto-Animate
- **Repo:** https://github.com/formkit/auto-animate
- **Stars:** 12K+
- **What:** One-line animations for lists.

### React Spring
- **Repo:** https://github.com/pmndrs/react-spring
- **Stars:** 28K+
- **What:** Physics-based animations.

### Theatre.js
- **Repo:** https://github.com/theatre-js/theatre
- **Stars:** 11K+
- **What:** Motion design editor.

### Atropos
- **Repo:** https://github.com/nolimits4web/atropos
- **What:** 3D parallax.

---

## Icons

### Lucide
- **Repo:** https://github.com/lucide-icons/lucide
- **Stars:** 10K+
- **What:** Beautiful, consistent icon set. Fork of Feather.
- **Why:** Default choice.

### Phosphor Icons
- **Repo:** https://github.com/phosphor-icons/web
- **Stars:** 3K+
- **What:** Multiple weights per icon.

### Heroicons
- **Repo:** https://github.com/tailwindlabs/heroicons
- **Stars:** 21K+
- **What:** From Tailwind team.

### Tabler Icons
- **Repo:** https://github.com/tabler/tabler-icons
- **Stars:** 18K+
- **What:** 5000+ free icons.

### Iconify
- **Repo:** https://github.com/iconify/iconify
- **Stars:** 4K+
- **What:** 200,000+ icons from many sets, on-demand.

### React Icons
- **Repo:** https://github.com/react-icons/react-icons
- **Stars:** 11K+
- **What:** Popular icon sets as React components.

### Material Symbols
- Google's icon set.

### Bootstrap Icons
- Free, comprehensive.

---

## Charts & Visualization

### Recharts
- **Repo:** https://github.com/recharts/recharts
- **Stars:** 23K+
- **What:** React charting library.
- **Why:** Easy. Composable.

### Tremor
- See Component Libraries. Dashboard-focused.

### Chart.js
- **Repo:** https://github.com/chartjs/Chart.js
- **Stars:** 64K+
- **What:** Most popular JS chart lib.

### D3.js
- **Repo:** https://github.com/d3/d3
- **Stars:** 108K+
- **What:** Low-level data viz.
- **When not:** Steep learning curve. Use Recharts/Visx for simple needs.

### Visx
- **Repo:** https://github.com/airbnb/visx
- **Stars:** 19K+
- **What:** Low-level visualization primitives for React.

### Victory
- **Repo:** https://github.com/FormidableLabs/victory
- **Stars:** 11K+
- **What:** React + React Native charts.

### Nivo
- **Repo:** https://github.com/plouc/nivo
- **Stars:** 13K+
- **What:** React dataviz components.

### Apache ECharts
- **Repo:** https://github.com/apache/echarts
- **Stars:** 60K+
- **What:** Powerful charting library.
- **Why:** Many chart types, performant.

### Highcharts
- **Repo:** https://github.com/highcharts/highcharts
- **What:** Commercial chart library.
- **When not:** Paid for commercial use.

### Plotly.js
- **Repo:** https://github.com/plotly/plotly.js
- **Stars:** 17K+
- **What:** Scientific charts.

### Observable Plot
- **Repo:** https://github.com/observablehq/plot
- **Stars:** 4K+
- **What:** Quick charts from D3 team.

### unovis
- **Repo:** https://github.com/f5/unovis
- **What:** Universal visualization.

### React Flow
- **Repo:** https://github.com/xyflow/xyflow
- **Stars:** 26K+
- **What:** Node-based UIs / diagrams.

---

## Tables

### TanStack Table
- **Repo:** https://github.com/TanStack/table
- **Stars:** 25K+
- **What:** Headless, type-safe table.
- **Why:** Default for serious tables.

### AG Grid
- **Repo:** https://github.com/ag-grid/ag-grid
- **Stars:** 12K+
- **What:** Enterprise data grid.
- **When not:** Free version is enough for most.

### Glide Data Grid
- **Repo:** https://github.com/glideapps/glide-data-grid
- **Stars:** 4K+
- **What:** High-performance spreadsheet-like grid.

### MUI DataGrid
- Part of MUI.

### react-data-table-component
- **Repo:** https://github.com/jbetancur/react-data-table-component

---

## Dates & Times

### date-fns
- **Repo:** https://github.com/date-fns/date-fns
- **Stars:** 34K+
- **What:** Modular date utility.
- **Why:** Tree-shakeable. Modern.

### Day.js
- **Repo:** https://github.com/iamkun/dayjs
- **Stars:** 46K+
- **What:** moment.js-compatible, 2KB.

### Luxon
- **Repo:** https://github.com/moment/luxon
- **Stars:** 15K+
- **What:** Modern moment alternative.

### Temporal API
- Built into JS (TC39 stage 3). Polyfill available.

---

## Utility Libraries

### Lodash
- **Repo:** https://github.com/lodash/lodash
- **Stars:** 59K+
- **What:** Utility functions.
- **When not:** Use native JS for most things now.

### Radash
- **Repo:** https://github.com/rayepps/radash
- **Stars:** 4K+
- **What:** Modern Lodash alternative, no deps.

### remeda
- **Repo:** https://github.com/remeda/remeda
- **Stars:** 4K+
- **What:** TS-first data-first utility library.

### clsx / classnames
- For conditional className strings.

### tailwind-merge
- **Repo:** https://github.com/dcastil/tailwind-merge
- **Why:** Merge Tailwind classes without conflicts. Pairs with `clsx`.

### cn utility (from shadcn/ui)
- `clsx` + `tailwind-merge` combined.

---

## Backend Frameworks (Node)

### Express
- **Repo:** https://github.com/expressjs/express
- **Stars:** 65K+
- **What:** Minimal Node web framework.
- **Why:** Most mature. Huge ecosystem.
- **When not:** Want speed (Fastify) or structure (NestJS).

### Fastify
- **Repo:** https://github.com/fastify/fastify
- **Stars:** 32K+
- **What:** High-performance Node framework.
- **Why:** 2x faster than Express. Schema-based.

### NestJS
- **Repo:** https://github.com/nestjs/nest
- **Stars:** 67K+
- **What:** Angular-style Node framework.
- **Why:** Enterprise structure. DI. TypeScript-first.

### Hono
- **Repo:** https://github.com/honojs/hono
- **Stars:** 20K+
- **What:** Ultrafast web framework for edges.
- **Why:** Runs on Cloudflare Workers, Bun, Deno, Node.
- **When not:** Already deep in Express.

### Elysia
- **Repo:** https://github.com/elysiajs/elysia
- **Stars:** 9K+
- **What:** Bun-first web framework.

### tRPC
- See above. Often the actual "backend" for TS apps.

### AdonisJS
- **Repo:** https://github.com/adonisjs/core
- **Stars:** 17K+
- **What:** Full-featured Node framework (Laravel-like).

### Sails.js
- **Repo:** https://github.com/balderdashy/sails
- **Status:** Legacy.

### Koa
- **Repo:** https://github.com/koajs/koa
- **Stars:** 35K+
- **What:** Express successor from same team. Less popular now.

### Polka
- **Repo:** https://github.com/lukeed/polka
- **What:** Express alternative, faster.

### tinyhttp
- **Repo:** https://github.com/tinyhttp/tinyhttp
- **What:** Modern Express alternative.

---

## Backend (Other Languages)

### Django
- **Repo:** https://github.com/django/django
- **Stars:** 78K+
- **What:** Batteries-included Python web framework.

### FastAPI
- **Repo:** https://github.com/fastapi/fastapi
- **Stars:** 73K+
- **What:** Async, typed Python API framework.
- **Why:** Modern Python default for APIs.

### Flask
- **Repo:** https://github.com/pallets/flask
- **Stars:** 67K+
- **What:** Minimal Python framework.

### Laravel
- **Repo:** https://github.com/laravel/laravel
- **Stars:** 78K+
- **What:** PHP framework. Eloquent, queues, etc.

### Symfony
- **Repo:** https://github.com/symfony/symfony
- **Stars:** 29K+
- **What:** Enterprise PHP framework.

### Rails
- **Repo:** https://github.com/rails/rails
- **Stars:** 55K+
- **What:** Ruby framework. Convention over configuration.

### Sinatra
- **Repo:** https://github.com/sinatra/sinatra
- **Stars:** 12K+
- **What:** Minimal Ruby framework.

### Gin (Go)
- **Repo:** https://github.com/gin-gonic/gin
- **Stars:** 77K+
- **What:** Fast Go web framework.

### Echo (Go)
- **Repo:** https://github.com/labstack/echo
- **Stars:** 29K+
- **What:** Go framework.

### Fiber (Go)
- **Repo:** https://github.com/gofiber/fiber
- **Stars:** 22K+
- **What:** Express-like Go framework.

### Chi (Go)
- **Repo:** https://github.com/go-chi/chi
- **Stars:** 18K+
- **What:** Lightweight Go router.

### Standard library net/http (Go)
- Often all you need.

### Axum (Rust)
- **Repo:** https://github.com/tokio-rs/axum
- **Stars:** 18K+
- **What:** Modular Rust web framework.

### Actix Web (Rust)
- **Repo:** https://github.com/actix/actix-web
- **Stars:** 21K+
- **What:** High-performance Rust framework.

### Rocket (Rust)
- **Repo:** https://github.com/rwf2/Rocket
- **Stars:** 24K+
- **What:** Ergonomic Rust framework.

### Spring Boot (Java)
- **Repo:** https://github.com/spring-projects/spring-boot
- **Stars:** 75K+
- **What:** Java enterprise framework.

### Quarkus (Java)
- **Repo:** https://github.com/quarkusio/quarkus
- **Stars:** 14K+
- **What:** Kubernetes-native Java.

### ASP.NET Core
- **Repo:** https://github.com/dotnet/aspnetcore
- **Stars:** 35K+
- **What:** C# web framework.

---

## Database Drivers & ORMs

### Prisma
- **Repo:** https://github.com/prisma/prisma
- **Stars:** 39K+
- **What:** Type-safe ORM with migrations + studio.
- **Why:** Best DX for most apps.

### Drizzle
- **Repo:** https://github.com/drizzle-team/drizzle-orm
- **Stars:** 22K+
- **What:** SQL-like TS ORM.
- **Why:** Lighter than Prisma. Edge-friendly.

### Kysely
- **Repo:** https://github.com/kysely-org/kysely
- **Stars:** 11K+
- **What:** Type-safe SQL query builder.

### TypeORM
- **Repo:** https://github.com/typeorm/typeorm
- **Stars:** 34K+
- **What:** Older TS ORM.
- **When not:** Use Prisma or Drizzle for new.

### Sequelize
- **Repo:** https://github.com/sequelize/sequelize
- **Stars:** 29K+
- **What:** Node ORM. Legacy.

### Mongoose
- **Repo:** https://github.com/Automattic/mongoose
- **Stars:** 27K+
- **What:** MongoDB ODM.

### pg (node-postgres)
- **Repo:** https://github.com/brianc/node-postgres
- **Stars:** 12K+
- **What:** Postgres driver for Node.

### postgres (porsager)
- **Repo:** https://github.com/porsager/postgres
- **Stars:** 6K+
- **What:** Modern Postgres driver.

### mysql2
- **Repo:** https://github.com/sidorares/node-mysql2

### ioredis
- **Repo:** https://github.com/redis/ioredis
- **Stars:** 14K+
- **What:** Redis client.

### node-redis
- **Repo:** https://github.com/redis/node-redis

### SQLAlchemy (Python)
- **Repo:** https://github.com/sqlalchemy/sqlalchemy
- **Stars:** 9K+
- **What:** Python SQL toolkit + ORM.

### Tortoise ORM (Python)
- **Repo:** https://github.com/tortoise/tortoise-orm
- **What:** Async Django-style ORM.

### Diesel (Rust)
- **Repo:** https://github.com/diesel-rs/diesel
- **Stars:** 12K+
- **What:** Rust ORM.

### sqlx (Rust)
- **Repo:** https://github.com/launchbadge/sqlx
- **Stars:** 13K+
- **What:** Async SQL for Rust, compile-time checked.

### GORM (Go)
- **Repo:** https://github.com/go-gorm/gorm
- **Stars:** 36K+
- **What:** Go ORM.

### sqlx (Go)
- **Repo:** https://github.com/jmoiron/sqlx
- **Stars:** 16K+
- **What:** Sqlx for Go.

### Entity Framework Core (.NET)
- **Repo:** https://github.com/dotnet/efcore
- **Stars:** 14K+
- **What:** .NET ORM.

### Active Record (Ruby)
- Built into Rails.

---

## Authentication

### NextAuth.js / Auth.js
- **Repo:** https://github.com/nextauthjs/next-auth
- **Stars:** 23K+
- **What:** Auth for Next.js. v5 is now Auth.js.
- **Why:** Default for Next apps.

### Lucia
- **Repo:** https://github.com/lucia-auth/lucia
- **Stars:** 9K+
- **What:** Simple, flexible auth library.
- **Status:** Author archived original; community maintaining.

### Clerk
- **Repo:** https://github.com/clerk/javascript
- **What:** Hosted auth UI + API. B2C SaaS friendly.
- **Why:** Ship fast. Beautiful UI.

### Auth0
- **What:** Enterprise auth service.

### Supabase Auth
- Built into Supabase. JWT + row-level security.

### Stytch
- **What:** Passwordless auth service.

### WorkOS
- **What:** Enterprise SSO / auth.

###better-auth
- **Repo:** https://github.com/better-auth/better-auth
- **Stars:** 5K+
- **What:** Comprehensive TS auth library.

### Ory
- **Repo:** https://github.com/ory
- **What:** Open-source identity platform.

### Keycloak
- **Repo:** https://github.com/keycloak/keycloak
- **Stars:** 23K+
- **What:** Open-source IAM.

### Passage by 1Password
- **What:** Passkeys-focused auth.

### oslo
- **Repo:** https://github.com/pilcrowonpaper/oslo
- **What:** Auth primitives (password hashing, random, JWT).

---

## Backend Tools

### BullMQ
- **Repo:** https://github.com/taskforcesh/bullmq
- **Stars:** 6K+
- **What:** Redis-based queue for Node.

### Temporal
- **Repo:** https://github.com/temporalio/temporal
- **Stars:** 12K+
- **What:** Durable execution / workflows.

### Bull
- Older version of BullMQ.

### Agenda
- **Repo:** https://github.com/agenda/agenda
- **What:** MongoDB-based job scheduler.

### node-cron
- **Repo:** https://github.com/node-cron/node-cron
- **What:** Cron for Node.

### Helmet
- **Repo:** https://github.com/helmetjs/helmet
- **Stars:** 9K+
- **What:** HTTP security headers middleware.

### CORS (Express)
- **Repo:** https://github.com/expressjs/cors

### Compression
- **Repo:** https://github.com/expressjs/compression

### Multer
- **Repo:** https://github.com/expressjs/multer
- **What:** File upload middleware.

### Pino
- **Repo:** https://github.com/pinojs/pino
- **Stars:** 14K+
- **What:** Fast structured logger.

### Winston
- **Repo:** https://github.com/winstonjs/winston
- **Stars:** 22K+
- **What:** Popular logger.

### Joi
- **Repo:** https://github.com/hapijs/joi
- **What:** Schema validation. Older.

### Express Validator
- **Repo:** https://github.com/express-validator/express-validator

### Argon2
- **Repo:** https://github.com/ranisalt/node-argon2
- **What:** Argon2 password hashing.

### bcrypt
- **Repo:** https://github.com/kelektiv/node.bcrypt.js
- **What:** bcrypt password hashing.

### jsonwebtoken
- **Repo:** https://github.com/auth0/node-jsonwebtoken
- **What:** JWT signing/verifying.

### jose
- **Repo:** https://github.com/panva/jose
- **What:** Modern JWT/JWE/JWS in TS.

---

## Databases & Hosting

### Postgres
- See [PostgreSQL/](PostgreSQL/).

### Supabase
- **Repo:** https://github.com/supabase/supabase
- **Stars:** 70K+
- **What:** Open-source Firebase alternative. Postgres + auth + storage + realtime.

### Neon
- **What:** Serverless Postgres. Branching.

### PlanetScale
- **What:** Serverless MySQL (was Postgres; now MySQL only on hobby? Check status).

### Turso
- **What:** SQLite on the edge. libSQL.

### Xata
- **What:** Postgres + search + files.

### Convex
- **What:** Reactive backend. Real-time DB.

### Fauna
- **What:** Serverless DB.

### MongoDB
- See [MongoDB/](MongoDB/).

### Redis
- See [Redis/](Redis/).

### Upstash
- **What:** Serverless Redis + Kafka + QStash.

### SQLite / libSQL / Turso
- See [SQLite/](SQLite/).

### ClickHouse
- **Repo:** https://github.com/ClickHouse/ClickHouse
- **Stars:** 36K+
- **What:** Columnar OLAP database.

### DuckDB
- **Repo:** https://github.com/duckdb/duckdb
- **Stars:** 23K+
- **What:** In-process OLAP.

### SurrealDB
- **Repo:** https://github.com/surrealdb/surrealdb
- **Stars:** 27K+
- **What:** Multi-model database.

---

## Vector Databases (for AI)

### pgvector
- **Repo:** https://github.com/pgvector/pgvector
- **Stars:** 11K+
- **What:** Vector extension for Postgres.
- **Why:** Default if you already have Postgres.

### Pinecone
- **What:** Managed vector DB.

### Qdrant
- **Repo:** https://github.com/qdrant/qdrant
- **Stars:** 19K+
- **What:** Open-source vector search.

### Weaviate
- **Repo:** https://github.com/weaviate/weaviate
- **Stars:** 11K+
- **What:** Open-source vector search.

### Chroma
- **Repo:** https://github.com/chroma-core/chroma
- **Stars:** 14K+
- **What:** AI-native vector DB.

### Milvus
- **Repo:** https://github.com/milvus-io/milvus
- **Stars:** 28K+
- **What:** Cloud-native vector DB.

### LanceDB
- **Repo:** https://github.com/lancedb/lancedb
- **Stars:** 4K+
- **What:** Multi-modal vector DB, embedded.

### AstraDB (DataStax)
- **What:** Managed vector DB on Cassandra.

---

## Testing

### Vitest
- See [Vitest/](Vitest/).

### Jest
- See [Jest/](Jest/).

### Playwright
- See [Playwright/](Playwright/).

### Cypress
- See [Cypress/](Cypress/).

### Testing Library
- **Repo:** https://github.com/testing-library/testing-library

### MSW
- **Repo:** https://github.com/mswjs/msw
- **Stars:** 15K+
- **What:** Mock Service Worker.

### Faker
- **Repo:** https://github.com/faker-js/faker
- **Stars:** 11K+
- **What:** Generate fake data.

### @ngneat/falso
- **Repo:** https://github.com/ngneat/falso
- **What:** Tree-shakeable faker.

### Storybook
- **Repo:** https://github.com/storybookjs/storybook
- **Stars:** 83K+
- **What:** Component dev environment.

### Ladle
- **Repo:** https://github.com/tajo/ladle
- **Stars:** 2K+
- **What:** Lighter Storybook alternative.

### Histoire
- **Repo:** https://github.com/histoire-dev/histoire
- **What:** Storybook for Vue.

### k6
- **Repo:** https://github.com/grafana/k6
- **Stars:** 25K+
- **What:** Load testing.

### Artillery
- **Repo:** https://github.com/artilleryio/artillery
- **Stars:** 8K+
- **What:** Load testing.

### Stryker (mutation testing)
- **Repo:** https://github.com/stryker-mutator/stryker
- **Stars:** 2.5K+

---

## Performance & Optimization

### Bundle Analyzer (Webpack)
- **Repo:** https://github.com/webpack-contrib/webpack-bundle-analyzer

### rollup-plugin-visualizer
- For Vite/Rollup.

### Size Limit
- **Repo:** https://github.com/ai/size-limit

### Lighthouse CI
- **Repo:** https://github.com/GoogleChrome/lighthouse-ci

### web-vitals
- **Repo:** https://github.com/GoogleChrome/web-vitals

### Partytown
- **Repo:** https://github.com/BuilderIO/partytown
- **Stars:** 12K+
- **What:** Run third-party scripts in a Web Worker.

### next-bundle-analyzer
- For Next.js.

---

## Accessibility

### axe-core
- **Repo:** https://github.com/dequelabs/axe-core
- **Stars:** 6K+
- **What:** A11y testing engine.

### eslint-plugin-jsx-a11y
- **Repo:** https://github.com/jsx-eslint/eslint-plugin-jsx-a11y

### @axe-core/playwright
- Axe in Playwright.

### react-aria
- See Component Libraries.

### focus-trap-react
- **Repo:** https://github.com/focus-trap/focus-trap-react

---

## SEO & Metadata

### next-sitemap
- **Repo:** https://github.com/iamvishnusankar/next-sitemap

### react-helmet-async
- **Repo:** https://github.com/staylor/react-helmet-async

### next-seo
- **Repo:** https://github.com/garmeeh/next-seo

### schema-dts
- **Repo:** https://github.com/google/schema-dts
- **What:** TypeScript types for Schema.org.

---

## Analytics

### PostHog
- **Repo:** https://github.com/PostHog/posthog
- **Stars:** 20K+
- **What:** Product analytics, feature flags, session replay.

### Plausible
- **Repo:** https://github.com/plausible/analytics
- **Stars:** 19K+
- **What:** Privacy-friendly analytics.

### Umami
- **Repo:** https://github.com/umami-software/umami
- **Stars:** 21K+
- **What:** Self-hosted web analytics.

### Fathom
- **What:** Privacy analytics, paid.

### Vercel Analytics
- Built into Vercel.

### Google Analytics 4
- The default (and privacy-invasive) option.

### Mixpanel
- Product analytics.

### Heap
- Auto-capture analytics.

### Sentry
- See Monitoring.

### Highlight.io
- **Repo:** https://github.com/highlight/highlight
- **What:** Open-source full-stack observability.

---

## Monitoring / Observability

### Sentry
- **Repo:** https://github.com/getsentry/sentry
- **Stars:** 38K+
- **What:** Error tracking + performance.

### OpenTelemetry
- **Repo:** https://github.com/open-telemetry
- **What:** Observability standard.

### Grafana
- **Repo:** https://github.com/grafana/grafana
- **Stars:** 62K+

### Prometheus
- **Repo:** https://github.com/prometheus/prometheus
- **Stars:** 54K+

### Loki
- **Repo:** https://github.com/grafana/loki
- **Stars:** 23K+

### Tempo
- **Repo:** https://github.com/grafana/tempo

### Jaeger
- **Repo:** https://github.com/jaegertracing/jaeger
- **Stars:** 20K+

### Datadog
- Commercial observability.

### New Relic
- Commercial observability.

### LogRocket
- Session replay + logs.

### Axiom
- **What:** Log management.

### Highlight.io
- See Analytics.

### BetterStack
- Uptime + logs.

### Uptime Kuma
- **Repo:** https://github.com/louislam/uptime-kuma
- **Stars:** 55K+
- **What:** Self-hosted uptime monitoring.

---

## Email

### Resend
- **Repo:** https://github.com/resend/resend-node
- **What:** Modern email API. DX-focused.

### Postmark
- **What:** Reliable transactional email.

### SendGrid
- **What:** Big transactional email.

### AWS SES
- **What:** Cheap email. More setup.

### Mailgun
- **What:** Transactional email.

### Plunk
- **Repo:** https://github.com/useplunk/plunk
- **What:** Open-source email.

### Loops
- **What:** Email for SaaS.

### React Email
- **Repo:** https://github.com/resend/react-email
- **Stars:** 14K+
- **What:** Build emails with React.

### MJML
- **Repo:** https://github.com/mjmlio/mjml
- **Stars:** 17K+
- **What:** Email template framework.

### Mailing
- **Repo:** https://github.com/sofn-oss/mailing
- **What:** React email templates.

---

## Payments

### Stripe
- **Repo:** https://github.com/stripe/stripe-node
- **What:** Default for online payments.

### Lemon Squeezy
- **What:** Merchant of record (handles VAT).

### Paddle
- **What:** Merchant of record.

### Polar
- **Repo:** https://github.com/polarsource/polar
- **What:** Open-source merchant of record for SaaS.

### Mollie
- **What:** EU-friendly payments.

### Razorpay
- **What:** India-focused payments.

---

## File Storage

### AWS S3
- Default object storage.

### Cloudflare R2
- **What:** S3-compatible, no egress fees.

### Backblaze B2
- **What:** Cheap S3-compatible.

### UploadThing
- **What:** File uploads for Next.js, easy.

### Supabase Storage
- Built into Supabase.

### Filebase
- **What:** Multi-backend storage.

---

## Search

### Meilisearch
- **Repo:** https://github.com/meilisearch/meilisearch
- **Stars:** 46K+
- **What:** Open-source search. Easy.

### Typesense
- **Repo:** https://github.com/typesense/typesense
- **Stars:** 21K+
- **What:** Open-source search. Fast.

### Algolia
- **What:** Managed search. Pricey at scale.

### Elasticsearch
- **Repo:** https://github.com/elastic/elasticsearch
- **Stars:** 68K+
- **What:** Search + analytics.

### OpenSearch
- **Repo:** https://github.com/opensearch-project/OpenSearch
- **Stars:** 9K+
- **What:** AWS fork of Elasticsearch.

### Orama
- **Repo:** https://github.com/oramasearch/orama
- **Stars:** 9K+
- **What:** In-memory full-text + vector search.

### Postgres Full-Text Search
- Built into Postgres. → [PostgreSQL/fts.md](PostgreSQL/fts.md)

---

## Realtime

### Socket.IO
- **Repo:** https://github.com/socketio/socket.io
- **Stars:** 61K+
- **What:** WebSocket library with fallbacks.

### ws
- **Repo:** https://github.com/websockets/ws
- **Stars:** 21K+
- **What:** Pure WebSocket library for Node.

### Ably
- **What:** Managed realtime.

### Pusher
- **What:** Managed realtime.

### Supabase Realtime
- Built into Supabase.

### Liveblocks
- **What:** Collaboration features.

### PartyKit (now Cloudflare)
- **What:** Edge realtime.

### Yjs
- **Repo:** https://github.com/yjs/yjs
- **Stars:** 16K+
- **What:** CRDT framework for collaboration.

### Automerge
- **Repo:** https://github.com/automerge/automerge
- **Stars:** 18K+
- **What:** CRDT library.

---

## AI / LLM

### Vercel AI SDK
- **Repo:** https://github.com/vercel/ai
- **Stars:** 9K+
- **What:** Streaming, tool calling, multi-provider.

### LangChain.js
- **Repo:** https://github.com/langchain-ai/langchainjs
- **Stars:** 13K+
- **What:** LLM framework.

### LlamaIndex
- **Repo:** https://github.com/run-llama/llama_index
- **Stars:** 36K+
- **What:** RAG framework.

### AI SDK by Vercel
- See above.

### @anthropic-ai/sdk
- Anthropic SDK.

### openai-node
- OpenAI SDK.

### replicate-js
- **Repo:** https://github.com/replicate/replicate-js
- **What:** Run models via Replicate.

### Ollama
- **Repo:** https://github.com/ollama/ollama
- **Stars:** 90K+
- **What:** Run LLMs locally.

### LM Studio
- **What:** Run LLMs locally, GUI.

### transformers.js
- **Repo:** https://github.com/huggingface/transformers.js
- **Stars:** 11K+
- **What:** Hugging Face transformers in JS.

### Instructor
- **Repo:** https://github.com/instructor-ai/instructor-js
- **What:** Structured extraction from LLMs.

### Outlines
- **Repo:** https://github.com/outlines-dev/outlines
- **Stars:** 9K+
- **What:** Structured generation (Python).

### DSPy
- **Repo:** https://github.com/stanfordnlp/dspy
- **Stars:** 17K+
- **What:** Programmatic LLM prompting (Python).

### Mastra
- **Repo:** https://github.com/mastra-ai/mastra
- **Stars:** 8K+
- **What:** TS-first AI agent framework.

### ModelFusion (now Vercel AI SDK)
- Merged into AI SDK.

### Codex / GPT-3.5/4
- See OpenAI.

---

## MCP Servers

### Model Context Protocol
- **Repo:** https://github.com/modelcontextprotocol
- **What:** Open standard for connecting LLMs to data/tools.

### Awesome MCP Servers
- **Repo:** https://github.com/modelcontextprotocol/servers
- **What:** Reference MCP server implementations (filesystem, GitHub, Slack, Postgres, etc.).

### MCP Hub
- Community-curated MCP servers.

---

## Agentic Coding Tools

### Cursor
- https://cursor.sh/

### Cline (formerly Claude Dev)
- **Repo:** https://github.com/cline/cline
- **Stars:** 10K+
- **What:** Open-source agentic VS Code extension.

### Aider
- **Repo:** https://github.com/Aider-AI/aider
- **Stars:** 15K+
- **What:** Terminal-based AI pair programmer.

### Continue
- **Repo:** https://github.com/continuedev/continue
- **Stars:** 20K+
- **What:** Open-source AI code assistant.

### OpenHands (formerly OpenDevin)
- **Repo:** https://github.com/All-Hands-AI/OpenHands
- **Stars:** 30K+
- **What:** Open-source autonomous agent.

### Devin
- https://devin.ai/ (commercial)

### GitHub Copilot
- https://github.com/features/copilot

### Codeium
- https://codeium.com/

### Tabnine
- https://www.tabnine.com/

### Sourcegraph Cody
- https://sourcegraph.com/cody

---

## Developer Tools / Utilities

### Husky
- **Repo:** https://github.com/typicode/husky
- Git hooks.

### lint-staged
- Lint only changed files.

### commitlint
- Enforce Conventional Commits.

### changesets
- **Repo:** https://github.com/changesets/changesets
- Versioning + changelogs.

### semantic-release
- Auto version + release.

### Biome
- **Repo:** https://github.com/biomejs/biome
- **Stars:** 14K+
- **What:** Lint + format in Rust.

### dprint
- Multi-language formatter.

### cross-env
- Cross-platform env vars in npm scripts.

### tsx
- **Repo:** https://github.com/privatenumber/tsx
- Run TS files directly.

### ts-node
- Older TS runner.

### Nodemon
- Restart node on file change.

### Concurrently
- Run multiple commands.

### npm-check-updates
- Update deps.

### knip
- **Repo:** https://github.com/webpro/knip
- Find unused files/exports/dependencies.

### distube
- Worker pools for Node.

---

## Templates / Boilerplates

### create-next-app
- `npx create-next-app@latest`

### create-t3-app
- **Repo:** https://github.com/t3-oss/create-t3-app
- **Stars:** 25K+
- **What:** Next + tRPC + Prisma + Tailwind + NextAuth.

### create-turbo
- Turborepo starter.

### shadcn/ui examples
- https://ui.shadcn.com/examples

### Epic Stack
- **Repo:** https://github.com/epicweb-dev/epic-stack
- **What:** Kent C. Dodds' production-ready stack.

### Indie Stack
- Remix/React Router + Tailwind + Prisma + SQLite.

### Bulletproof React
- **Repo:** https://github.com/alan2207/bulletproof-react
- **Stars:** 28K+
- **What:** Scalable React architecture.

### Vue Vine
- **What:** Vue starter.

### Astro Starlight
- Docs template.

---

## Monorepo

### Turborepo
- **Repo:** https://github.com/vercel/turbo
- **Stars:** 26K+
- **What:** Build system for monorepos.

### Nx
- **Repo:** https://github.com/nrwl/nx
- **Stars:** 23K+
- **What:** Monorepo build system.

### pnpm workspaces
- Built into pnpm.

### Lerna
- Older monorepo tool. Mostly replaced by Nx/Turbo.

### Changesets
- See above. For monorepo versioning.

---

## Internationalization (i18n)

### next-intl
- **Repo:** https://github.com/amannn/next-intl

### i18next + react-i18next
- **Repo:** https://github.com/i18next/react-i18next
- **Stars:** 9K+
- **What:** Most popular i18n library.

### FormatJS
- **Repo:** https://github.com/formatjs/formatjs

### Lingui
- **Repo:** https://github.com/lingui/js-lingui

### Paraglide
- **Repo:** https://github.com/inlingu/paraglide
- **What:** Modern, minimal i18n.

### typesafe-i18n
- **Repo:** https://github.com/ivanhofer/typesafe-i18n

---

## Static Site Generators

### Astro
- See above.

### Eleventy (11ty)
- **Repo:** https://github.com/11ty/eleventy
- **Stars:** 17K+
- **What:** Simple SSG.

### Gatsby
- **Repo:** https://github.com/gatsbyjs/gatsby
- **Stars:** 55K+
- **Status:** Legacy. Use Astro or Next.

### Hugo
- **Repo:** https://github.com/gohugoio/hugo
- **Stars:** 75K+
- **What:** Go-based SSG. Fast.

### Jekyll
- **Repo:** https://github.com/jekyll/jekyll
- **Stars:** 49K+
- **What:** Ruby SSG. GitHub Pages native.

### MkDocs
- **Repo:** https://github.com/mkdocs/mkdocs
- **What:** Python docs SSG.

### VitePress
- **Repo:** https://github.com/vuejs/vitepress
- **Stars:** 12K+
- **What:** Vue-powered docs SSG.

### Docusaurus
- **Repo:** https://github.com/facebook/docusaurus
- **Stars:** 55K+
- **What:** React docs SSG.

### Nextra
- **Repo:** https://github.com/shuding/nextra
- **Stars:** 11K+
- **What:** Next.js docs SSG.

### Astro Starlight
- **Repo:** https://github.com/withastro/starlight
- **What:** Astro docs template.

---

## Boilerplates / Starters (more)

### SAAS Starter Kit
- **Repo:** https://github.com/Nextjs-Boilerplate/nextjs-boilerplate
- Next.js + auth + Stripe + Drizzle.

### Makerkit
- Paid SaaS starter.

### Supastarter
- Paid Supabase SaaS starter.

### Vercel Templates
- https://vercel.com/templates

### Shadcn Templates
- Various community templates.

---

## Markdown / Rich Text

### Unified / Remark / Rehype
- **Repo:** https://github.com/unifiedjs/unified
- **What:** Markdown processing pipeline.

### MDX
- **Repo:** https://github.com/mdx-js/mdx
- **Stars:** 17K+
- **What:** Markdown + JSX.

### Contentlayer
- **Repo:** https://github.com/contentlayerdev/contentlayer
- **Status:** Maintenance. Consider next-mdx-remote or fumadocs.

### Fumadocs
- **Repo:** https://github.com/fuma-nama/fumadocs
- **What:** Next.js docs framework.

### TipTap
- **Repo:** https://github.com/ueberdosis/tiptap
- **Stars:** 27K+
- **What:** Headless rich text editor.

### Lexical
- **Repo:** https://github.com/facebook/lexical
- **Stars:** 18K+
- **What:** Meta's text editor framework.

### ProseMirror
- **Repo:** https://github.com/ProseMirror/prosemirror
- **Stars:** 8K+
- **What:** Customizable rich text editor framework.

### Slate
- **Repo:** https://github.com/ianstormtaylor/slate
- **Stars:** 30K+
- **What:** Rich text editor framework.

### Editor.js
- **Repo:** https://github.com/codex-team/editor.js
- **What:** Block-style editor.

---

## Maps

### MapLibre GL
- **Repo:** https://github.com/maplibre/maplibre-gl-js
- **Stars:** 6K+
- **What:** Open-source fork of Mapbox GL.

### Mapbox GL JS
- Commercial maps.

### Leaflet
- **Repo:** https://github.com/Leaflet/Leaflet
- **Stars:** 41K+
- **What:** Simple maps.

### react-leaflet
- React bindings.

### vis.gl/react-google-maps
- Official Google Maps React bindings.

### Deck.gl
- **Repo:** https://github.com/visgl/deck.gl
- **Stars:** 12K+
- **What:** Geospatial visualization.

### Tangram
- 3D maps.

---

## Video / Audio

### Mux
- Video API.

### Cloudflare Stream
- Video.

### Video.js
- **Repo:** https://github.com/videojs/video.js
- **Stars:** 37K+
- **What:** HTML5 video player.

### Plyr
- **Repo:** https://github.com/sampotts/plyr
- **Stars:** 26K+
- **What:** Media player.

### hls.js
- **Repo:** https://github.com/video-dev/hls.js
- **Stars:** 14K+
- **What:** HLS playback.

### FFmpeg.wasm
- FFmpeg in browser.

### Tone.js
- **Repo:** https://github.com/Tonejs/Tone.js
- **What:** Web Audio framework.

### Howler.js
- **Repo:** https://github.com/goldfire/howler.js
- **Stars:** 24K+
- **What:** Audio library.

---

## Security & Crypto

### Helmet (Node)
- See Backend Tools.

### bcrypt / argon2
- See Backend Tools.

### jose / jsonwebtoken
- See Backend Tools.

### DOMPurify
- **Repo:** https://github.com/cure53/DOMPurify
- **Stars:** 13K+
- **What:** XSS sanitizer for HTML.

### sanitize-html
- **Repo:** https://github.com/apostrophecms/sanitize-html

### OAuth libraries
- `oauth` / `simple-oauth2` / `openid-client`.

### csrf
- **Repo:** https://github.com/pillarjs/csrf

### express-rate-limit
- **Repo:** https://github.com/express-rate-limit/express-rate-limit

---

## DevOps & Deployment

### Docker
- See [Docker/](Docker/).

### Kubernetes
- See [Kubernetes/](Kubernetes/).

### Helm
- **Repo:** https://github.com/helm/helm
- K8s package manager.

### Argo CD
- **Repo:** https://github.com/argoproj/argo-cd
- GitOps for K8s.

### Flux
- **Repo:** https://github.com/fluxcd/flux2
- GitOps for K8s.

### Terraform
- **Repo:** https://github.com/hashicorp/terraform
- IaC.

### Pulumi
- **Repo:** https://github.com/pulumi/pulumi
- IaC with real languages.

### OpenTofu
- **Repo:** https://github.com/opentofu/opentofu
- Open-source Terraform fork.

### Ansible
- **Repo:** https://github.com/ansible/ansible
- Config management.

### Vagrant
- **Repo:** https://github.com/hashicorp/vagrant
- Dev envs.

### Dev Containers
- https://containers.dev/

### Coolify
- **Repo:** https://github.com/coollabsio/coolify
- **Stars:** 30K+
- **What:** Self-hosted Vercel/Heroku alternative.

### Dokploy
- **Repo:** https://github.com/Dokploy/dokploy
- Open-source PaaS.

### CapRover
- **Repo:** https://github.com/caprover/caprover
- Self-hosted PaaS.

### Easypanel
- Modern PaaS.

---

## Awesome Lists (Master References)

- **Awesome:** https://github.com/sindresorhus/awesome
- **Awesome React:** https://github.com/enaqx/awesome-react
- **Awesome Vue:** https://github.com/vuejs/awesome-vue
- **Awesome Angular:** https://github.com/PatrickJS/awesome-angular
- **Awesome Svelte:** https://github.com/TheComputerM/awesome-svelte
- **Awesome Node.js:** https://github.com/sindresorhus/awesome-nodejs
- **Awesome CSS:** https://github.com/awesome-css-group/awesome-css
- **Awesome Tailwind:** https://github.com/aniftyco/awesome-tailwindcss
- **Awesome TypeScript:** https://github.com/semlinker/awesome-typescript
- **Awesome Python:** https://github.com/vinta/awesome-python
- **Awesome Go:** https://github.com/avelino/awesome-go
- **Awesome Rust:** https://github.com/rust-unofficial/awesome-rust
- **Awesome Ruby:** https://github.com/markets/awesome-ruby
- **Awesome Java:** https://github.com/akullpp/awesome-java
- **Awesome .NET:** https://github.com/quozd/awesome-dotnet
- **Awesome PHP:** https://github.com/ziadoz/awesome-php
- **Awesome Postgres:** https://github.com/dhamaniasad/awesome-postgres
- **Awesome Redis:** https://github.com/JamzyWang/awesome-redis
- **Awesome Docker:** https://github.com/veggiemonk/awesome-docker
- **Awesome Kubernetes:** https://github.com/ramitsurana/awesome-kubernetes
- **Awesome DevOps:** https://github.com/joelparkerhenderson/awesome-devops
- **Awesome Security:** https://github.com/sbilly/awesome-security
- **Awesome AppSec:** https://github.com/paragonie/awesome-appsec
- **Awesome AI:** https://github.com/owainlewis/awesome-artificial-intelligence
- **Awesome LLM:** https://github.com/Hannibal046/Awesome-LLM
- **Awesome Generative AI:** https://github.com/steven2358/awesome-generative-ai
- **Awesome MCP:** https://github.com/modelcontextprotocol/awesome-mcp-servers
- **Awesome Agentic:** https://github.com/e2b-dev/awesome-ai-agents
- **Awesome Prompts:** https://github.com/f/awesome-chatgpt-prompts
- **Awesome Self-Hosted:** https://github.com/awesome-selfhosted/awesome-selfhosted
- **Awesome Design:** https://github.com/gztchan/awesome-design
- **Awesome Design Systems:** https://github.com/alexpate/awesome-design-systems
- **Awesome Accessibility:** https://github.com/brunopulis/awesome-a11y
- **Awesome Performance:** https://github.com/hbfnucleo/awesome-web-performance
- **Awesome SEO:** https://github.com/teles/awesome-seo
- **Awesome Testing:** https://github.com/TheJambo/awesome-testing

---

**Next:** [INDEX.md](INDEX.md) · [AI_AGENT_GUIDE.md](AI_AGENT_GUIDE.md) · [START-HERE.md](START-HERE.md)
