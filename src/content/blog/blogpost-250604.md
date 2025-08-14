---
title: Get in Loser, we're going Shopping with Dude Scouts
description: The Boy Scouts meets silly goose energy meets coding
pubDate: 2025-06-04 9:20
author: Kevin Coyle
tags:
  - Adventure
  - Full Stack Development
imgUrl: '../../assets/dude-scouts.png'
layout: ../../layouts/BlogPost.astro
---

# How about more features?

Since no one asked, let's build a headless Shopify ecommerce site. 

## Mock Shop, Real UX: From Analytics Integration to a Dynamic Badge Storefront

Between my last commit and now, I've added a mock badge shop with dynamic product pages. I shifted from backend observability to a tangible, user-facing feature: a shoppable badge catalog with dynamic routes, basic SEO, and authentication hooks. Here’s what shipped, why it matters, and how it’s set up under the hood.

## Logins

All this makes me think: I need to stop dragging my feet, I need add a login with auth. I'll use Clerk for this because it's the only thing I know to do besides spinning something up from scratch.

### What we built

- Mock badge shop with dynamic product pages
  - New route `"/shop"` lists products using a reusable `ProductList` and `ProductCard`.
  - Dynamic product pages at `"/shop/[slug]"` read from `mockTrails` and render details, simple gallery, and an “Add to Cart” stub.
  - Per-page SEO via Next.js `generateMetadata`, ensuring shareable titles/descriptions.

- Navigation + Auth integration
  - `Navigation` now includes a Shop link.
  - Auth with Clerk: `SignedIn/Out`, modal `SignInButton`/`SignUpButton`, and `UserButton` wired into `layout.tsx` and `Navigation.tsx`.
  - Vercel env config updated for Clerk keys.

- Deployability and performance enhancements
  - Next.js `output: 'standalone'` for smaller, optimized Docker images.
  - Production compose and scripts added/enhanced for cleaner CI/CD upgrades.

### Key files added or changed

- Pages and components
  - Added `src/app/shop/page.tsx` for catalog page and `src/app/shop/[slug]/page.tsx` for dynamic product details.
  - `src/components/mockshop/ProductList.tsx` and `ProductCard.tsx` compose a simple, consistent grid UI.
  - `src/app/layout.tsx` wraps the app with `ClerkProvider`.
  - `src/components/Navigation.tsx` exposes auth actions and a Shop entry.

- Config and infra
  - `next.config.js`: `output: 'standalone'` to support lean Docker images. I learned this trick from a developer while I was working at Marriott to do multi-stage builds. This has sped up my build times quite a bit.
  - Docker-related: I did some `docker-compose.yml` tweaks, and a production compose was introduced.

### A quick look at the dynamic product page

```src/app/shop/[slug]/page.tsx
export async function generateMetadata({ params }) {
  const product = mockTrails.find((p) => p.slug === params.slug);
  if (!product) return { title: "Product Not Found" };
  return {
    title: `${product.displayTitle} | Dude Scouts Shop`,
    description: product.description,
  };
}

export default function ProductPage({ params }) {
  const product = mockTrails.find((p) => p.slug === params.slug);
  if (!product) notFound();

  const images = [product.badgeImage, product.badgeImage, product.badgeImage];

  return (
    <div className="min-h-screen bg-white">
      <Navigation />
      {/* Product card, gallery, price, CTA */}
    </div>
  );
}
```

### Why this matters

- Validates the commerce UX: Even as a mock, this flow exercises product discovery, detail pages, and cart affordances, de-risking future Shopify/Stripe wiring.
- SEO-friendly catalog: `generateMetadata` gives us meaningful titles and descriptions per product, improving shareability and search engine readiness.
- Auth-ready: With Clerk integrated, we can quickly gate purchase flows, favorites, and order history behind real sessions.
- Cloud-native builds: The standalone Next.js output simplifies Docker deploys and trims runtime footprint.

### What’s next

- Replace mock data with a real product source
  - Drop-in options exist (`src/components/shopify/` and `src/lib/shopify.ts` have scaffolding).
- Add analytics events on shop interactions
  - Reuse the Snowplow pattern from the backend to capture “view_product”, “add_to_cart”, etc.
- Wire payments and checkout
  - Stripe or Shopify checkout; progressively enhance the mock UI with real flows.
- Harden CI/CD
  - Use the production compose for preview/staging. Keep Clerk and Snowplow

This iteration takes Dude Scouts from internal visibility (Snowplow) to a visible, testable storefront experience. It lays the groundwork for real commerce with minimal rework while maintaining production-friendly deployment practices.