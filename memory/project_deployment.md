---
name: Deployment & Launch Strategy
description: Both sites live on Cloudflare Pages with noindex. Merge to main triggers rebuild. Git dependency for shared lib until first npm publish.
type: project
---

## Deployment Pipeline
- Each site connected to Cloudflare Pages via GitHub repo
- Merge to `main` triggers automatic rebuild and deploy
- Both sites are live and accessible:
  - chuckallen.dev → also at chuckallen-dev.pages.dev
  - chuckallen.ai → also at chuckallen-ai.pages.dev

## Pre-Launch SEO Block
- All pages have `<meta name="robots" content="noindex,nofollow">` (BaseLayout default)
- Remove per-site when Chuck says it's ready for search engines

## Shared Library Dependency
- Currently using git dependency: `"@mrwpress/shared": "github:mrwpress/chuck-allen-shared"`
- npm publish workflow is configured (NPM_TOKEN secret set)
- Once first GitHub Release is created on chuck-allen-shared, it auto-publishes to npm
- After that, switch sites to versioned: `"@mrwpress/shared": "^0.1.0"`
- To update shared lib in a site: `npm update @mrwpress/shared` then restart dev server

## Cloudflare Pages Build
- Build command: `npm run build`
- Output directory: `dist`
- Node version: 22
- No auth needed for dependencies (npm public registry + public GitHub repo for git dep)

**Why:** Building in production lets Chuck preview real builds. Sites shouldn't be indexed until content and design are finalized.

**How to apply:** Every merge to main deploys. To update shared components in a deployed site, update the shared repo first, then `npm update` in the site and merge.
