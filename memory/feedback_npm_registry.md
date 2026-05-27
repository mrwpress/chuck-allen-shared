---
name: npm Public Registry Decision
description: @mrwpress/shared published to npm public registry, not GitHub Packages — required for Cloudflare Pages builds
type: feedback
---

`@mrwpress/shared` is published to the **npm public registry** (registry.npmjs.org), NOT GitHub Packages.

**Why:** GitHub Packages requires authentication even for public packages. Cloudflare Pages (and any CI environment) would need a `NODE_AUTH_TOKEN` configured to pull dependencies. The npm public registry requires zero auth — `npm install` just works everywhere.

**How to apply:** 
- The shared repo's `publishConfig` points to `https://registry.npmjs.org` with `"access": "public"`
- The GitHub Action uses `NPM_TOKEN` secret (not `GITHUB_TOKEN`) to publish
- All site `.npmrc` files point to `registry.npmjs.org`
- The publish workflow file (`publish.yml`) requires a token with `workflow` scope to push — Chuck needs to add this manually or update his GitHub token scopes
