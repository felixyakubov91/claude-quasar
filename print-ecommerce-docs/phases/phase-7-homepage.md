# Phase 7: Homepage & Marketing

## Overview
Build the marketing homepage and implement comprehensive SEO optimization.

## Duration
Days 24-26

## Goals
- Build dynamic homepage with CMS content
- Optimize SEO across all pages
- Integrate Google Analytics 4

## Tasks
| Task | File | Description |
|------|------|-------------|
| 7.1 | `tasks/7.1-homepage.md` | Hero, featured products, categories |
| 7.2 | `tasks/7.2-seo-optimization.md` | Meta tags, sitemap, robots.txt |
| 7.3 | `tasks/7.3-analytics.md` | GA4 setup with e-commerce tracking |

## Prerequisites
- Phase 6 completed
- Strapi homepage content type created
- Google Analytics account

## Homepage Sections

### Hero Banner
- Full-width banner image/video
- Headline text (RTL-aware)
- Subheadline
- CTA button(s)
- Multiple slides (carousel)
- Editable in Strapi

### Featured Products
- 4-8 featured products
- Product cards with quick add
- "View All" link
- Sorted by `is_featured` flag

### Category Showcase
- Visual category grid
- Category images
- Product count per category
- Hover effects

### Promotional Sections
- Sale banner
- New arrivals
- Best sellers
- Custom promotional blocks

### Trust Signals
- Customer testimonials
- Partner logos
- Quality guarantees
- Secure payment badges

### Newsletter Signup
- Email input
- Privacy notice
- Integration with email provider

## Strapi Homepage Content Type

```javascript
// Single Type: Homepage
{
  hero_slides: [
    {
      image: 'media',
      headline_en: 'string',
      headline_he: 'string',
      subheadline_en: 'string',
      subheadline_he: 'string',
      cta_text_en: 'string',
      cta_text_he: 'string',
      cta_link: 'string',
    }
  ],
  featured_products: 'relation -> Product, many',
  featured_categories: 'relation -> Category, many',
  promotional_blocks: [
    {
      type: 'enum: sale, new, custom',
      title_en: 'string',
      title_he: 'string',
      content_en: 'richtext',
      content_he: 'richtext',
      image: 'media',
      link: 'string',
    }
  ],
  testimonials: [
    {
      customer_name: 'string',
      content_en: 'text',
      content_he: 'text',
      rating: 'integer',
      avatar: 'media',
    }
  ],
  seo: {
    meta_title: 'string',
    meta_description: 'text',
    og_image: 'media',
  }
}
```

## SEO Implementation

### Meta Tags (every page)
```html
<title>Page Title | Brand Name</title>
<meta name="description" content="...">
<meta name="robots" content="index, follow">
<link rel="canonical" href="https://...">

<!-- Open Graph -->
<meta property="og:title" content="...">
<meta property="og:description" content="...">
<meta property="og:image" content="...">
<meta property="og:url" content="...">
<meta property="og:type" content="website">
<meta property="og:locale" content="he_IL">

<!-- Twitter -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="...">
<meta name="twitter:description" content="...">
```

### Structured Data (JSON-LD)

```javascript
// Organization
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "Print Company",
  "url": "https://...",
  "logo": "https://...",
  "contactPoint": {
    "@type": "ContactPoint",
    "telephone": "+972-...",
    "contactType": "customer service"
  }
}

// Product (product pages)
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "...",
  "image": "...",
  "description": "...",
  "offers": {
    "@type": "Offer",
    "price": "49.99",
    "priceCurrency": "ILS",
    "availability": "https://schema.org/InStock"
  },
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "4.5",
    "reviewCount": "24"
  }
}

// BreadcrumbList
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [...]
}
```

### Sitemap.xml
- Generated dynamically
- Includes all products, categories
- Updated on content changes
- Submitted to Google Search Console

### robots.txt
```
User-agent: *
Allow: /
Disallow: /profile/
Disallow: /cart/
Disallow: /checkout/
Sitemap: https://example.com/sitemap.xml
```

## Google Analytics 4

### E-commerce Events
- `view_item_list` - Product listing viewed
- `view_item` - Product detail viewed
- `add_to_cart` - Item added to cart
- `remove_from_cart` - Item removed
- `begin_checkout` - Checkout started
- `add_shipping_info` - Shipping selected
- `add_payment_info` - Payment started
- `purchase` - Order completed

### Custom Events
- `search` - Search performed
- `apply_coupon` - Coupon applied
- `login` - User logged in
- `sign_up` - User registered
- `share` - Content shared

## Files Created After Phase 7
```
frontend/src/
├── pages/
│   └── IndexPage.vue          # Homepage
├── components/
│   └── home/
│       ├── HeroSlider.vue
│       ├── FeaturedProducts.vue
│       ├── CategoryShowcase.vue
│       ├── PromotionalBlock.vue
│       ├── Testimonials.vue
│       └── NewsletterSignup.vue
├── boot/
│   └── analytics.ts           # GA4 initialization
├── composables/
│   └── useAnalytics.ts        # Analytics helpers
└── public/
    ├── robots.txt
    └── sitemap.xml            # Generated

backend/src/
└── api/
    └── homepage/              # Single type
```

## Acceptance Criteria
- [ ] Homepage loads with all sections
- [ ] Hero slider cycles through slides
- [ ] Featured products display correctly
- [ ] Categories show with product counts
- [ ] Testimonials rotate or display
- [ ] All content editable in Strapi
- [ ] Meta tags render correctly (SSR)
- [ ] Open Graph tags work (test with debugger)
- [ ] JSON-LD validates (Google Rich Results Test)
- [ ] sitemap.xml accessible and valid
- [ ] robots.txt configured correctly
- [ ] GA4 events fire correctly
- [ ] E-commerce tracking works in GA4
- [ ] Lighthouse SEO score > 90
- [ ] Mobile performance acceptable
