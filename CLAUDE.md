# @mrwpress/shared — Shared Component Library

## What this is
Shared Astro component library published as `@mrwpress/shared` on GitHub Packages. Used by all Chuck Allen sites (chuckallen.dev, chuckallen.ai, and future domains).

## Rules
- **Performance first** — every decision filtered through performance impact
- **No CSS frameworks** — all CSS is component-scoped via Astro `<style>` blocks
- **All components accept `site: SiteConfig` prop** for site-level data (NAP, nav, social, keys)
- **Header/Footer use `<slot name="logo" />`** so each site provides its own logo
- **Images must use `<Picture />` from `astro:assets`** — AVIF + WebP, proper loading attributes
- **Never push to main** — always branch → PR → merge
- **TypeScript strict mode**, ESNext target

## Publishing
GitHub Action auto-publishes on Release creation. Sites install via `npm install @mrwpress/shared`.

## Memory
The `memory/` folder mirrors the global Claude project memory from `~/.claude/projects/`. Keep it synced when memory is updated.
