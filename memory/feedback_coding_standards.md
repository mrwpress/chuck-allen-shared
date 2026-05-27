---
name: Coding Standards & Preferences
description: Chuck's coding conventions — Astro, scoped CSS, TypeScript, performance-first, image optimization rules
type: feedback
---

## PERFORMANCE FIRST
Performance is the top priority on every decision. Every choice — images, CSS, scripts, third-party loads — must be evaluated through a performance lens first.

## Tech Stack Defaults (all sites unless otherwise stated)
- **Framework:** Astro (static SSG) — zero JS overhead, pre-rendered
- **Styling:** No CSS frameworks (no Tailwind, Bootstrap, etc.). All CSS is component-scoped via Astro `<style>` blocks. Global CSS only when explicitly discussed.
- **Language:** TypeScript (strict mode, ESNext target)
- **Deployment:** Cloudflare Pages + Workers for serverless functions
- **No external linting/testing/formatting tools** — no ESLint, Prettier, Jest, Husky, etc.

## Image Rules
- **ALL raster images** must live in `src/assets/` (NOT `public/`) so Astro can process them
- **Always use `<Picture />` component** from `astro:assets` — generates AVIF + WebP formats automatically
- Above-fold images: `loading="eager"` + `fetchpriority="high"`
- Below-fold images: `loading="lazy"` + `decoding="async"`
- Decorative images: `alt=""` + `aria-hidden="true"`
- SVGs can live in `public/` (they don't need processing)
- Never serve unoptimized PNGs/JPGs to the browser

## Naming Conventions
- Components: **PascalCase** (e.g., `Header.astro`, `Hero.astro`)
- Config/utility files: **camelCase** (e.g., `site.ts`, `navigation.ts`)
- CSS classes: **kebab-case** (e.g., `section-container`, `grid-bg`)
- Data attributes: **camelCase** (e.g., `data-items`)
- HTML IDs: **kebab-case** (e.g., `mobile-menu-toggle`)
- Variables/functions: **camelCase**
- Pages: **kebab-case** or directory-based routing

## Component Patterns
- Self-contained Astro components with co-located `<style>` and `<script>` blocks
- TypeScript `interface Props` for component props, destructured with defaults from `Astro.props`
- ESM imports at top of frontmatter
- Script event listener pattern: `document.addEventListener('astro:page-load', () => { ... })`
- DOM type assertions: `const el = document.querySelector(...) as HTMLElement`

## CSS/Styling Patterns
- **No CSS frameworks** — pure CSS in component-scoped `<style>` blocks
- Mobile-first responsive design with media queries
- Inline `style` attributes only for dynamic/computed values
- Animations defined in component `<style>` blocks with `@keyframes`
- CSS custom properties for design tokens (from shared tokens.css)

## Config Patterns
- Single `SiteConfig` object per site in `src/config/site.ts` (typed via @mrwpress/shared)
- Covers NAP, SEO defaults, nav, social links, third-party keys — one file, one source of truth
- `as const` assertions for immutable config objects

## Accessibility
- Comprehensive ARIA labels on nav, sections, icons
- Semantic HTML elements (section, nav, main, etc.)
- `aria-hidden="true"` for decorative elements

## Performance Rules
- Inline stylesheets (`build.inlineStylesheets: 'always'`)
- Asset inlining up to 100KB
- Deferred GTM loading (requestIdleCallback → setTimeout fallback)
- Edge redirects via Cloudflare (301s at CDN level)
- Scroll-padding-top for fixed headers
- GPU-accelerated CSS animations (transforms, will-change)
- Preload critical fonts (Inter WOFF2)
- Minimize third-party scripts; lazy-load when possible (e.g., Turnstile loaded on chat open)

## Project Structure (per site)
```
src/
├── assets/images/     # ALL raster images here (Astro Picture processed)
├── components/        # Site-specific .astro components
├── layouts/           # Site layout wrapping shared BaseLayout
├── pages/             # Route pages
├── config/            # site.ts (SiteConfig)
├── content/           # Content collections (blog, etc.)
└── styles/            # Site-specific global overrides (if any)
functions/             # Cloudflare Workers (serverless API)
public/                # SVGs, favicons, _redirects, fonts
```

**Why:** Chuck values performance above all, development velocity, minimal dependencies, and maximum page speed. Every byte counts.

**How to apply:** When writing code for Chuck's projects, performance is the first filter. Use Astro `<Picture />` for all images, component-scoped CSS, co-located scripts, and strict TypeScript. Never introduce CSS frameworks, unoptimized images, or unnecessary dependencies.
