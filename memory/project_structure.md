---
name: Project Structure - Chuck Allen Multi-Site
description: chuck-allen is a multi-domain project with subfolders per domain, each with its own git repo, plus a shared npm component library
type: project
---

The `/Users/batman/Sites/chuck-allen/` directory is a parent folder containing multiple domain-specific projects, each in its own subfolder with its own GitHub repo.

## Domains (both live on Cloudflare Pages)
- **chuckallen.dev/** → GitHub: mrwpress/chuckallen.dev (public) → https://chuckallen.dev
  - Red/black palette (#dc2626 accent, #09090b bg)
  - Personal developer brand — "hire me" site
- **chuckallen.ai/** → GitHub: mrwpress/chuckallen.ai (public) → https://chuckallen.ai
  - Orange/black palette (#ea580c accent, #0a0a0a bg)
  - Umbrella company brand — modern technical consultancy

## Shared Library
- **shared/** → GitHub: mrwpress/chuck-allen-shared (public)
- Published as `@mrwpress/shared` on npm public registry
- Currently consumed via git dependency: `"github:mrwpress/chuck-allen-shared"`
- Will switch to versioned npm dep once first Release is created
- `.npmrc` in each site points to registry.npmjs.org

### Shared Library Contents
```
shared/src/
├── components/
│   ├── BadgeWheel.astro    # iOS-style rolling badge picker (desktop wheel + mobile marquee)
│   ├── Contact.astro       # Contact section + chat modal (Turnstile + form, div with inline display toggle)
│   ├── Footer.astro        # Footer with nav, social, legal, copyright
│   ├── GridBackground.astro # Decorative grid + blobs
│   ├── Header.astro        # Fixed header + mobile nav slide-out
│   └── SEOHead.astro       # Meta tags, OG, Twitter Card
├── fonts/                   # Inter 400-700 WOFF2
├── layouts/
│   └── BaseLayout.astro    # HTML shell, SEO, schema, GTM, font preload, noindex default
├── styles/
│   ├── tokens.css          # Design tokens (CSS custom properties) — teal defaults, overridden per site
│   ├── reset.css           # Base reset + global defaults
│   ├── prose.css           # Markdown content styling
│   └── utilities.css       # Buttons, cards, grid-bg, blobs, forms, marquee
└── utils/
    ├── config.ts           # SiteConfig type definition (single source of truth)
    ├── schema.ts           # Schema.org structured data generators
    └── index.ts            # Re-exports
```

### Per-Site Structure
```
site/
├── astro.config.ts         # Sitemap, inline stylesheets, asset inlining
├── src/
│   ├── config/site.ts      # SiteConfig — NAP, nav, social, SEO, keys
│   ├── layouts/Layout.astro # Wraps BaseLayout + Header + Footer with site logo
│   ├── pages/index.astro   # Single-page: Hero, Services, Work, About, Contact
│   └── styles/global.css   # Imports shared tokens/reset/utilities + palette overrides + font faces
├── public/
│   ├── fonts/              # Inter WOFF2 files
│   └── images/             # Badge SVGs, favicons
├── CLAUDE.md
├── .gitignore              # Tracks .claude/ intentionally
└── .npmrc
```

### Publishing Workflow
- GitHub Action auto-publishes @mrwpress/shared on Release (NPM_TOKEN secret required)
- Merge to main triggers Cloudflare Pages rebuild on each site

### Key Patterns
- All shared components accept `site: SiteConfig` prop
- Header and Footer use `<slot name="logo" />` for site-specific logos
- Color palettes overridden per-site via CSS custom property redefinition in global.css
- Chat modal uses inline `style="display:none"` + JS toggle (Astro scoped CSS specificity workaround)
- BadgeWheel on desktop is wrapped in a site-level `.hero-wheel` div; mobile marquee in `.hero-marquee-mobile`

**How to apply:** Each subfolder is an independent project with its own git repo. The parent `chuck-allen/` is NOT a git repo. Reusable components go in `shared/`. Site-specific components stay in that site's `src/components/`.
