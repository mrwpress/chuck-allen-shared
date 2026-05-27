---
name: Site Architecture - Single Page Model
description: Each site is a single scrollable page with anchor sections, not multi-page. Blog on subdomain if ever needed.
type: feedback
---

Each site follows a **single-page scrollable model** — one `index.astro` with anchor sections (hero, services, work, contact, etc.). Not a true SPA (no client-side JS routing), just a single pre-rendered HTML page.

Separate pages only for legal requirements (privacy, terms).

If blogging is ever added, it goes on a **subdomain** (e.g., `blog.chuckallen.dev`), not on the main domain.

**Why:** Target audience (devs/agencies) wants to scan quickly. One continuous narrative is faster, more performant, and keeps contact always one scroll away. Avoids unnecessary page loads and JS overhead.

**How to apply:** Don't create multi-page navigation structures. Each site's core experience is a single `index.astro` composing section components. Nav links use anchor hrefs (`/#services`, `/#contact`). Legal pages are the only separate routes.
