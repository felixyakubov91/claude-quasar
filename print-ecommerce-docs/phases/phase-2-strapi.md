# Phase 2: Strapi Backend Setup

## Overview
Configure Strapi CMS with all content types, permissions, and integrations.

## Duration
Days 4-6

## Goals
- Create all content types (Products, Categories, Orders, etc.)
- Configure user roles and permissions
- Set up Supabase auth webhook integration
- Configure Strapi plugins
- Seed initial sample data

## Tasks
| Task | File | Description |
|------|------|-------------|
| 2.1 | `tasks/2.1-strapi-content-types.md` | Create all content types and components |
| 2.2 | `tasks/2.2-strapi-permissions.md` | Configure roles and permissions |
| 2.3 | `tasks/2.3-auth-webhook.md` | Supabase → Strapi user sync webhook |
| 2.4 | `tasks/2.4-strapi-plugins.md` | Configure i18n, SEO, upload plugins |
| 2.5 | `tasks/2.5-seed-data.md` | Seed categories, products, shipping zones |

## Prerequisites
- Phase 1 completed
- Strapi running locally
- PostgreSQL database configured

## Content Types to Create

### Collection Types
1. **Product** - Printable products with options
2. **Category** - Hierarchical product categories
3. **Customer** - Synced from Supabase Auth
4. **Order** - Customer orders
5. **Order Item** - Line items in orders
6. **Coupon** - Discount codes
7. **Review** - Product reviews
8. **Uploaded Image** - Customer uploaded files
9. **Cart** - Persistent shopping carts
10. **Shipping Zone** - Delivery regions and rates

### Single Types
1. **Homepage** - Hero banners, featured sections

### Components
1. **ProductOption** - Size, paper, finish options
2. **PricingTier** - Quantity-based pricing
3. **Address** - Shipping/billing addresses
4. **ShippingRate** - Weight-based shipping rates

## Permission Matrix

| Role | Products | Categories | Orders | Cart | Reviews | Customers |
|------|----------|------------|--------|------|---------|-----------|
| Public | Read | Read | - | - | Read | - |
| Authenticated | Read | Read | Create/Read own | CRUD own | Create | Read own |
| Admin | CRUD | CRUD | CRUD | CRUD | CRUD | CRUD |

## Files Created After Phase 2
```
backend/
├── src/
│   ├── api/
│   │   ├── product/
│   │   │   ├── content-types/product/schema.json
│   │   │   ├── controllers/product.js
│   │   │   ├── routes/product.js
│   │   │   └── services/product.js
│   │   ├── category/
│   │   ├── customer/
│   │   ├── order/
│   │   ├── order-item/
│   │   ├── coupon/
│   │   ├── review/
│   │   ├── uploaded-image/
│   │   ├── cart/
│   │   ├── shipping-zone/
│   │   └── homepage/
│   └── components/
│       ├── product-option/
│       ├── pricing-tier/
│       ├── address/
│       └── shipping-rate/
├── config/
│   └── plugins.js
└── database/
    └── seeds/
        ├── categories.json
        ├── products.json
        └── shipping-zones.json
```

## Acceptance Criteria
- [ ] All content types visible in Strapi admin
- [ ] Relations work correctly (Product → Category, Order → Customer)
- [ ] Components are reusable (ProductOption in Product)
- [ ] Public can read products/categories without auth
- [ ] Authenticated users can create orders
- [ ] Supabase signup triggers customer creation in Strapi
- [ ] Sample data visible in admin
