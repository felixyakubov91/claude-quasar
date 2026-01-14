# Print E-commerce Platform - Documentation Overview

## Quick Start

This documentation is designed to be fed to Claude Code for implementation. Each file is self-contained with all necessary context.

## Architecture Summary

```
Frontend: Vue 3 + Quasar (SSR)    →  SEO-optimized storefront
Auth:     Supabase Auth           →  OAuth, Magic Links, Email
Backend:  Strapi v4               →  CMS + API + Admin Panel
Database: PostgreSQL (Strapi)     →  All business data
Images:   Cloudinary              →  Upload, transform, CDN
Storage:  Vultr Object Storage    →  Archival
Payments: PayPlus                 →  Israeli payment processing
Email:    Resend                  →  Transactional emails
Hosting:  Vultr Cloud Compute     →  VPS deployment
```

## Implementation Phases

| Phase | Focus | Files |
|-------|-------|-------|
| **1** | Project Setup & Foundation | `phases/phase-1-setup.md` |
| **2** | Strapi Backend Setup | `phases/phase-2-strapi.md` |
| **3** | Product Catalog | `phases/phase-3-catalog.md` |
| **4** | Image Upload & Editor | `phases/phase-4-upload.md` |
| **5** | Shopping Cart & Checkout | `phases/phase-5-checkout.md` |
| **6** | User Profile & Orders | `phases/phase-6-profile.md` |
| **7** | Homepage & Marketing | `phases/phase-7-homepage.md` |
| **8** | Admin & Polish | `phases/phase-8-polish.md` |

## Task Files

Each task file in `tasks/` can be fed directly to Claude Code. They contain:
- Clear task description
- Prerequisites
- Step-by-step instructions
- Code snippets
- Files to create
- Acceptance criteria

## How to Use

1. **Start a new Claude Code session**
2. **Feed the relevant task file** as your prompt
3. **Claude will implement** based on the detailed instructions
4. **Verify acceptance criteria** before moving to next task

## Project Structure

```
print-ecommerce/
├── frontend/          # Quasar SSR app
│   ├── src/
│   │   ├── boot/      # Initialization (supabase, strapi, i18n)
│   │   ├── pages/     # Route pages
│   │   ├── components/# Vue components
│   │   ├── composables/# Vue composables
│   │   ├── stores/    # Pinia stores
│   │   ├── services/  # API services
│   │   └── i18n/      # Translations
│   └── src-ssr/       # SSR server
├── backend/           # Strapi CMS
│   └── src/api/       # Content types
├── scripts/           # Deployment & cloning
└── docker-compose.yml # Container config
```

## Key Requirements

- RTL/Hebrew support with `postcss-rtlcss`
- SSR for SEO (Lighthouse score >90)
- Mobile-first responsive design
- Product reviews
- Advanced image editor (crop, filters, text)
- Coupon system
- Easy cloning for new clients
