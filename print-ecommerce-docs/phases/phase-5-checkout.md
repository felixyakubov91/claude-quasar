# Phase 5: Shopping Cart & Checkout

## Overview
Build the complete shopping cart and checkout flow with payment integration.

## Duration
Days 16-20

## Goals
- Build cart functionality with persistence
- Implement coupon system
- Create checkout flow with address forms
- Integrate PayPlus payment
- Build order confirmation with email

## Tasks
| Task | File | Description |
|------|------|-------------|
| 5.1 | `tasks/5.1-cart-functionality.md` | Cart store, add/remove, persistence |
| 5.2 | `tasks/5.2-coupon-system.md` | Coupon validation and application |
| 5.3 | `tasks/5.3-checkout-flow.md` | Address forms, shipping selection |
| 5.4 | `tasks/5.4-payplus-integration.md` | PayPlus payment integration |
| 5.5 | `tasks/5.5-order-confirmation.md` | Confirmation page + email via Resend |

## Prerequisites
- Phase 4 completed
- PayPlus account with API credentials
- Resend account with verified domain

## Cart Flow

```
┌──────────────────┐
│  Add to Cart     │
│  (product page)  │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│  Cart Drawer     │
│  (slide out)     │
├──────────────────┤
│  - Items list    │
│  - Quantities    │
│  - Remove        │
│  - Subtotal      │
│  - Coupon input  │
│  - Checkout btn  │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│  Cart Page       │
│  (full view)     │
├──────────────────┤
│  - Edit items    │
│  - Upload images │
│  - Price summary │
│  - Continue btn  │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│  Checkout        │
├──────────────────┤
│  Step 1: Address │
│  Step 2: Shipping│
│  Step 3: Review  │
│  Step 4: Payment │
└──────────────────┘
```

## Cart Data Structure

```typescript
interface CartItem {
  id: string;
  productId: number;
  product: Product;          // Populated product data
  quantity: number;
  selectedOptions: {
    size?: string;
    paper?: string;
    finish?: string;
    [key: string]: string;
  };
  unitPrice: number;         // Calculated with options
  totalPrice: number;        // unitPrice * quantity
  uploadedImages: UploadedImage[];
  notes?: string;
}

interface Cart {
  items: CartItem[];
  subtotal: number;
  discount: number;
  couponCode?: string;
  shippingCost: number;
  tax: number;
  total: number;
}
```

## Coupon Logic

```typescript
function applyCoupon(cart: Cart, coupon: Coupon): CouponResult {
  // Validate coupon
  if (!coupon.is_active) return { error: 'Coupon inactive' };
  if (coupon.valid_from > now) return { error: 'Coupon not yet valid' };
  if (coupon.valid_until < now) return { error: 'Coupon expired' };
  if (coupon.usage_count >= coupon.usage_limit) return { error: 'Coupon limit reached' };
  if (cart.subtotal < coupon.minimum_order) return { error: 'Minimum not met' };

  // Check product/category restrictions
  if (coupon.applicable_products.length > 0) {
    // Only apply to specific products
  }

  // Calculate discount
  let discount = 0;
  switch (coupon.discount_type) {
    case 'percentage':
      discount = cart.subtotal * (coupon.discount_value / 100);
      if (coupon.maximum_discount) {
        discount = Math.min(discount, coupon.maximum_discount);
      }
      break;
    case 'fixed':
      discount = coupon.discount_value;
      break;
    case 'free_shipping':
      discount = cart.shippingCost;
      break;
  }

  return { success: true, discount };
}
```

## PayPlus Integration

```typescript
// 1. Create payment page
const response = await payplus.createPaymentPage({
  payment_page_uid: process.env.PAYPLUS_PAGE_UID,
  charge_method: 1, // Credit card
  amount: order.total,
  currency_code: 'ILS',
  sendEmailApproval: true,
  sendEmailFailure: true,
  customer: {
    customer_name: customer.full_name,
    email: customer.email,
    phone: customer.phone,
  },
  items: order.items.map(item => ({
    name: item.product_name,
    quantity: item.quantity,
    price: item.unit_price,
  })),
  more_info: order.id,
  success_url: `${BASE_URL}/checkout/confirmation?order=${order.id}`,
  failure_url: `${BASE_URL}/checkout/payment?error=failed`,
  callback_url: `${STRAPI_URL}/api/orders/payment-webhook`,
});

// 2. Redirect to PayPlus
window.location.href = response.data.payment_page_link;

// 3. Handle webhook (Strapi controller)
async paymentWebhook(ctx) {
  const { transaction_uid, status_code, more_info } = ctx.request.body;

  if (status_code === '000') { // Success
    await strapi.entityService.update('api::order.order', more_info, {
      data: {
        payment_status: 'paid',
        payment_reference: transaction_uid,
        paid_at: new Date(),
        status: 'confirmed',
      },
    });

    // Send confirmation email
    await sendOrderConfirmation(more_info);
  }
}
```

## Files Created After Phase 5
```
frontend/src/
├── pages/
│   ├── cart/
│   │   └── IndexPage.vue
│   └── checkout/
│       ├── IndexPage.vue
│       ├── PaymentPage.vue
│       └── ConfirmationPage.vue
├── components/
│   ├── cart/
│   │   ├── CartItem.vue
│   │   ├── CartSummary.vue
│   │   ├── CouponInput.vue
│   │   └── CartDrawer.vue
│   └── checkout/
│       ├── ShippingForm.vue
│       ├── ShippingMethodSelector.vue
│       ├── PaymentForm.vue
│       ├── UpsPickupMap.vue
│       └── OrderSummary.vue
├── stores/
│   └── cart.store.ts
├── services/
│   └── payment.service.ts
├── composables/
│   ├── useCart.ts
│   └── useCoupons.ts

backend/src/
├── api/order/
│   └── controllers/order.js  # Payment webhook handler
└── extensions/
    └── email/               # Resend integration
```

## Acceptance Criteria
- [ ] Add to cart works from product page
- [ ] Cart drawer shows correctly
- [ ] Quantities can be updated
- [ ] Items can be removed
- [ ] Cart persists after page reload
- [ ] Guest cart stored in localStorage
- [ ] Logged-in user cart syncs with Strapi
- [ ] Coupon validation works (all rules)
- [ ] Discount calculates correctly
- [ ] Checkout form validates inputs
- [ ] Address autocomplete works (optional)
- [ ] Shipping methods load based on zone
- [ ] PayPlus redirect works
- [ ] Payment success updates order
- [ ] Confirmation email sends
- [ ] Confirmation page shows order details
