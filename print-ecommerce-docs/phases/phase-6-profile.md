# Phase 6: User Profile & Orders

## Overview
Build user account management, order history, and product review functionality.

## Duration
Days 21-23

## Goals
- Build user profile management
- Create order history and tracking
- Implement product review system

## Tasks
| Task | File | Description |
|------|------|-------------|
| 6.1 | `tasks/6.1-user-profile.md` | Profile page, addresses, settings |
| 6.2 | `tasks/6.2-order-history.md` | Order list, detail, tracking |
| 6.3 | `tasks/6.3-review-system.md` | Reviews CRUD, display on products |

## Prerequisites
- Phase 5 completed
- Authentication working
- Orders can be created

## User Profile Features

### Account Info
- Full name (editable)
- Email (display only, change via Supabase)
- Phone number
- Preferred language (en-US / he)
- Avatar image

### Address Management
- List saved addresses
- Add new address
- Edit existing address
- Delete address
- Set default address
- Address labels (Home, Office, etc.)

### Security
- Change password (via Supabase)
- View active sessions
- Delete account

## Order History Features

### Order List
- Paginated order history
- Order number, date, status, total
- Filter by status
- Search by order number
- Quick re-order button

### Order Detail
- Full order information
- Line items with images
- Selected options per item
- Uploaded images per item
- Shipping address
- Payment info (masked)
- Status timeline
- Tracking number with carrier link
- Download invoice (PDF)

### Order Statuses
1. `pending` - Order placed, awaiting payment
2. `confirmed` - Payment received
3. `processing` - Order being prepared
4. `printing` - Items being printed
5. `shipped` - Out for delivery
6. `delivered` - Successfully delivered
7. `cancelled` - Order cancelled
8. `refunded` - Payment refunded

## Review System Features

### Writing Reviews
- Star rating (1-5)
- Title
- Review content
- Only for delivered orders
- One review per product per customer

### Displaying Reviews
- Average rating on product card
- Review count
- Individual reviews on product page
- Helpful/not helpful voting
- Sort by date, rating, helpfulness
- Verified purchase badge

### Admin Moderation
- Reviews require approval
- Flag inappropriate content
- Respond to reviews

## Data Structures

```typescript
interface UserProfile {
  id: string;
  supabase_id: string;
  email: string;
  full_name: string;
  phone: string;
  preferred_language: 'en-US' | 'he';
  avatar_url?: string;
  addresses: Address[];
  created_at: string;
}

interface Address {
  id: string;
  label: string;
  full_name: string;
  street_address: string;
  city: string;
  postal_code: string;
  country: string;
  phone: string;
  is_default: boolean;
}

interface Review {
  id: number;
  customer: Customer;
  product: Product;
  rating: number;
  title: string;
  content: string;
  is_approved: boolean;
  is_verified_purchase: boolean;
  helpful_count: number;
  created_at: string;
}
```

## Files Created After Phase 6
```
frontend/src/
├── pages/
│   └── profile/
│       ├── IndexPage.vue      # Profile overview
│       ├── OrdersPage.vue     # Order history list
│       ├── OrderDetailPage.vue # Single order detail
│       └── SettingsPage.vue   # Account settings
├── components/
│   ├── profile/
│   │   ├── ProfileInfo.vue
│   │   ├── AddressList.vue
│   │   ├── AddressForm.vue
│   │   └── LanguageSelector.vue
│   ├── orders/
│   │   ├── OrderList.vue
│   │   ├── OrderCard.vue
│   │   ├── OrderTimeline.vue
│   │   └── OrderItemRow.vue
│   └── products/
│       ├── ProductReviews.vue
│       ├── ReviewCard.vue
│       ├── ReviewForm.vue
│       └── RatingStars.vue
├── composables/
│   ├── useAuth.ts
│   ├── useOrders.ts
│   └── useReviews.ts
└── types/
    ├── user.ts
    └── order.ts
```

## Acceptance Criteria
- [ ] Profile info displays correctly
- [ ] Profile can be edited
- [ ] Addresses can be CRUD
- [ ] Default address selection works
- [ ] Language preference persists
- [ ] Order history loads with pagination
- [ ] Order detail shows all information
- [ ] Status timeline shows progress
- [ ] Tracking link opens carrier site
- [ ] Re-order adds items to cart
- [ ] Reviews can be submitted
- [ ] Reviews display on product page
- [ ] Average rating calculates correctly
- [ ] Verified purchase badge shows
- [ ] Reviews require admin approval
