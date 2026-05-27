---
name: SEO & Analytics Patterns
description: Chuck's SEO structured data, meta tags, analytics, and layout patterns from mrwp-redesign
type: feedback
---

## Layout SEO Props
```typescript
interface Props {
  title?: string;
  description?: string;
  canonicalUrl?: string;
  ogImage?: string;
  ogType?: 'website' | 'article';
  articlePublished?: string;
  articleModified?: string;
  noindex?: boolean;
  schema?: Record<string, unknown>;
}
```

## Structured Data (Schema.org)
- Organization (ProfessionalService) on every page
- WebSite schema on every page
- WebPage or Article schema (conditional on page type)
- BreadcrumbList (dynamically generated from URL path)

## Meta Tags
- Open Graph (Facebook/LinkedIn): title, description, image, type
- Twitter Card support
- Canonical URLs

## Analytics
- Google Tag Manager loaded via deferred strategy:
  - `requestIdleCallback` if available, else `setTimeout(fn, 50)`
  - Only loads after page is complete (past Lighthouse measurement window)
- Partytown integration available for third-party script isolation

## Font Loading
- Inter font (400, 500, 600, 700) preloaded as WOFF2
- System font fallback stack: `'Inter', system-ui, -apple-system, sans-serif`
- `font-smoothing: antialiased`

**Why:** Performance-conscious SEO — structured data for rich results, deferred analytics to protect Core Web Vitals.

**How to apply:** Every new page should include proper meta tags, Schema.org data, and follow the deferred analytics pattern. Use the Layout component's props interface for SEO configuration.
