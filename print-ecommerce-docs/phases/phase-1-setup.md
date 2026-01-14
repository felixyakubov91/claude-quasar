# Phase 1: Project Setup & Foundation

## Overview
Set up the foundational infrastructure for the printing e-commerce platform.

## Duration
Days 1-3

## Goals
- Initialize Quasar project with SSR mode
- Initialize Strapi backend
- Configure RTL support for Hebrew
- Set up Supabase authentication
- Configure environment variables
- Create base layouts and routing

## Tasks
| Task | File | Description |
|------|------|-------------|
| 1.1 | `tasks/1.1-init-quasar.md` | Initialize Quasar with SSR, Pinia, TypeScript |
| 1.2 | `tasks/1.2-init-strapi.md` | Initialize Strapi v4 with PostgreSQL |
| 1.3 | `tasks/1.3-configure-rtl.md` | RTL support with postcss-rtlcss + Hebrew |
| 1.4 | `tasks/1.4-setup-supabase.md` | Supabase auth configuration |
| 1.5 | `tasks/1.5-env-variables.md` | Environment variable setup |
| 1.6 | `tasks/1.6-base-layouts.md` | MainLayout, AuthLayout, routing |

## Prerequisites
- Node.js 18+ installed
- PostgreSQL installed or available
- Supabase account created
- Cloudinary account created

## Key Decisions
- **SSR Mode**: Required for SEO
- **TypeScript**: For type safety
- **Pinia**: Official Vue 3 state management
- **vue-i18n**: For internationalization

## Files Created After Phase 1
```
print-ecommerce/
├── frontend/
│   ├── quasar.config.js
│   ├── postcss.config.js
│   ├── package.json
│   ├── tsconfig.json
│   ├── .env.example
│   ├── src/
│   │   ├── App.vue
│   │   ├── boot/
│   │   │   ├── supabase-auth.ts
│   │   │   ├── strapi.ts
│   │   │   ├── i18n.ts
│   │   │   └── quasar-lang.ts
│   │   ├── css/
│   │   │   ├── app.scss
│   │   │   ├── quasar.variables.scss
│   │   │   └── rtl-overrides.scss
│   │   ├── i18n/
│   │   │   ├── en-US/index.ts
│   │   │   └── he/index.ts
│   │   ├── layouts/
│   │   │   ├── MainLayout.vue
│   │   │   ├── AuthLayout.vue
│   │   │   └── CheckoutLayout.vue
│   │   └── router/
│   │       ├── index.ts
│   │       └── routes.ts
│   └── src-ssr/
│       └── server.ts
├── backend/
│   ├── package.json
│   ├── config/
│   │   ├── database.js
│   │   └── server.js
│   └── src/
└── supabase/
    └── config.toml
```

## Acceptance Criteria
- [ ] `npm run dev` starts Quasar SSR successfully
- [ ] Hebrew language pack loads correctly
- [ ] RTL layout flips properly when `lang="he"`
- [ ] Strapi admin accessible at `localhost:1337/admin`
- [ ] Supabase auth client initializes without errors
- [ ] Environment variables load in both dev and SSR modes
