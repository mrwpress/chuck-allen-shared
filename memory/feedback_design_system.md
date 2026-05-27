---
name: Shared Design System
description: Design tokens, visual language, and component library for all Chuck Allen sites — per-site palette overrides via CSS custom properties
type: feedback
---

The shared library (`@mrwpress/shared`) contains a complete design system:

## Styles (`src/styles/`)
- **tokens.css** — CSS custom properties (colors, spacing, radii, transitions, shadows). Defaults are teal (from mrwpress.com). Each site overrides in its own global.css.
- **reset.css** — Box-sizing, font smoothing, element resets
- **prose.css** — Markdown/blog content styling (.prose class)
- **utilities.css** — Reusable patterns: .section-container, .btn-primary, .btn-outline, .card, .grid-bg, .blob, .input, .marquee, .divider

## Components (`src/components/`)
- **BadgeWheel.astro** — iOS-style rolling badge picker. Desktop: vertical wheel with magnified center slot, auto-cycles every 2.5s. Mobile: infinite horizontal marquee. Accepts `items` array of `{ label, icon }`.
- **Header.astro** — Fixed header, desktop nav, mobile hamburger + slide-out panel, email CTA. Logo via `<slot name="logo" />`
- **Footer.astro** — Logo, nav links, social icons, legal links, email, copyright. All colors use tokens (no hardcoded values).
- **Contact.astro** — Contact cards (call, email, book, message) + chat modal with Turnstile CAPTCHA. Modal uses `<div style="display:none">` + JS toggle.
- **GridBackground.astro** — Decorative grid lines, floating blocks, ambient glow blobs. Default blob color uses `var(--color-accent-dim)`.
- **SEOHead.astro** — Title, meta description, canonical, OG tags, Twitter Card. `noindex` defaults to true.

## Per-Site Palette Override Pattern
Each site redefines CSS custom properties in its `global.css` after importing shared tokens:
```css
@import '@mrwpress/shared/styles/tokens.css';
:root {
  --color-accent: #dc2626;      /* site-specific */
  --color-accent-light: #ef4444;
  --color-accent-dim: rgba(220, 38, 38, 0.12);
  --color-bg: #09090b;
  /* etc */
}
```

## Current Palettes
- **mrwpress.com** — Teal/dark blue (#00769d accent, #07080e bg)
- **chuckallen.dev** — Red/black (#dc2626 accent, #09090b bg)
- **chuckallen.ai** — Orange/black (#ea580c accent, #0a0a0a bg)

## Known Gotcha
Astro's scoped CSS has higher specificity than HTML `hidden` attribute and class-based `display:none`. For visibility toggling (like the chat modal), use **inline `style="display:none"`** on the element and toggle via `el.style.display` in JS. Do NOT rely on `hidden` attribute or CSS classes for show/hide.

**How to apply:** Each site imports shared styles, overrides the palette tokens, and all components automatically pick up the new colors. No component modifications needed per site. New shared components must use `var(--color-*)` tokens exclusively — never hardcode color values.
