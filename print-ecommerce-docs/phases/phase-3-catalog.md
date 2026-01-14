# Phase 3: Product Catalog

## Overview
Build the customer-facing product browsing experience with filtering, sorting, and SEO.

## Duration
Days 7-10

## Goals
- Create Strapi service layer for frontend
- Build product listing pages with filtering/sorting
- Build product detail page with options
- Implement SEO with meta tags and structured data

## Tasks
| Task | File | Description |
|------|------|-------------|
| 3.1 | `tasks/3.1-strapi-service.md` | Create strapi.service.ts with API methods |
| 3.2 | `tasks/3.2-product-listing.md` | All products page + category pages |
| 3.3 | `tasks/3.3-product-detail.md` | Product detail page with options |
| 3.4 | `tasks/3.4-seo-implementation.md` | Meta tags, JSON-LD, sitemap |

## Prerequisites
- Phase 2 completed
- Strapi has sample products
- Quasar SSR running

## Key Components

### ProductCard.vue
- Thumbnail image
- Product name (RTL-aware)
- Price display (sale price if applicable)
- Quick add to cart button
- Category badge

### ProductFilters.vue
- Category tree filter
- Price range slider
- Paper type filter
- Size filter
- In stock only toggle

### ProductGrid.vue
- Responsive grid (1-4 columns)
- List/grid view toggle
- Loading skeletons
- Empty state

### ProductGallery.vue
- Main image display
- Thumbnail navigation
- Zoom on hover
- Fullscreen lightbox

### ProductOptions.vue
- Size selector
- Paper type selector
- Finish selector
- Quantity input with tier pricing
- Live price calculation

## API Endpoints Used

```typescript
// Get all products with filters
GET /api/products?filters[category][slug][$eq]=business-cards
    &filters[base_price][$gte]=10
    &filters[base_price][$lte]=100
    &sort=base_price:asc
    &pagination[page]=1
    &pagination[pageSize]=12
    &populate=*

// Get single product
GET /api/products?filters[slug][$eq]=premium-business-cards
    &populate[category]=*
    &populate[options]=*
    &populate[pricing_tiers]=*
    &populate[images]=*
    &populate[reviews]=*

// Get categories
GET /api/categories?filters[is_active][$eq]=true
    &populate[parent]=*
    &populate[products][count]=true
```

## SEO Implementation

### Meta Tags (useSeo composable)
```typescript
useSeo({
  title: product.name_he || product.name_en,
  description: product.short_description_he || product.short_description_en,
  image: product.thumbnail?.url,
  type: 'product'
});
```

### JSON-LD Structured Data
```json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "Premium Business Cards",
  "description": "High-quality business cards...",
  "image": "https://...",
  "offers": {
    "@type": "Offer",
    "price": "49.99",
    "priceCurrency": "ILS",
    "availability": "InStock"
  }
}
```

## Files Created After Phase 3
```
frontend/src/
├── services/
│   └── strapi.service.ts
├── pages/
│   └── products/
│       ├── IndexPage.vue        # All products
│       ├── CategoryPage.vue     # Category listing
│       └── [slug].vue           # Product detail
├── components/
│   └── products/
│       ├── ProductCard.vue
│       ├── ProductGrid.vue
│       ├── ProductFilters.vue
│       ├── ProductGallery.vue
│       ├── ProductOptions.vue
│       └── PriceCalculator.vue
├── composables/
│   ├── useProducts.ts
│   └── useSeo.ts
└── stores/
    └── products.store.ts
```

## Acceptance Criteria
- [ ] Products load via SSR (view-source shows content)
- [ ] Filtering by category, price works
- [ ] Sorting by price, name, date works
- [ ] Pagination loads more products
- [ ] Product detail shows all options
- [ ] Price updates when options change
- [ ] RTL layout correct for Hebrew
- [ ] Meta tags render correctly
- [ ] Lighthouse SEO score > 90
