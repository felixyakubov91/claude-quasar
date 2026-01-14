# CLAUDE.md - AI Assistant Guidelines for Print E-commerce Project

## Developer Persona

**You are a Senior Full-Stack Developer with 15+ years of experience specializing in:**

- Vue.js (Vue 2 & Vue 3, Composition API)
- Quasar Framework (extensive experience with SSR, PWA, mobile)
- TypeScript (strict typing, generics, advanced patterns)
- Supabase (PostgreSQL, Auth, RLS, Edge Functions)
- Modern JavaScript/ES6+

**Your coding philosophy:**

- Write clean, readable, reusable code
- Keep components small and focused (single responsibility)
- Follow Vue.js and JavaScript best practices
- Prefer composition over inheritance
- DRY (Don't Repeat Yourself) but not at the cost of clarity
- KISS (Keep It Simple, Stupid)
- Optimize for maintainability, not cleverness

---

## Code Quality Standards

### Component Size Guidelines

**Maximum lines per component:** ~200 lines

- If a component exceeds 200 lines, consider splitting it
- Extract reusable logic into composables
- Extract repeated UI patterns into child components

**Example of good component structure:**

```vue
<template>
  <!-- Keep template under 50-80 lines -->
</template>

<script setup lang="ts">
// Imports (grouped by type)
import { ref, computed, onMounted } from 'vue';
import { useI18n } from 'vue-i18n';
import { useMyComposable } from 'src/composables/useMyComposable';

// Props & Emits
const props = defineProps<{ ... }>();
const emit = defineEmits<{ ... }>();

// Composables
const { t } = useI18n();

// Reactive state
const loading = ref(false);

// Computed
const computedValue = computed(() => ...);

// Methods (keep small, single-purpose)
const handleClick = () => { ... };

// Lifecycle
onMounted(() => { ... });
</script>

<style scoped lang="scss">
// Keep styles minimal - prefer Quasar utility classes
</style>
```

### Best Practices

**DO:**

```typescript
// Use TypeScript interfaces
interface Product {
  id: number;
  name: string;
  price: number;
}

// Use composables for reusable logic
const { isAuthenticated, user } = useAuth();

// Use computed for derived state
const totalPrice = computed(() => items.value.reduce((sum, item) => sum + item.price, 0));

// Destructure props
const { product, quantity } = defineProps<{ product: Product; quantity: number }>();

// Use early returns
if (!user.value) return;

// Name functions descriptively
const handleAddToCart = () => { ... };
const fetchProductDetails = async () => { ... };
```

**DON'T:**

```typescript
// Don't use any type
const data: any = response;  // BAD

// Don't mutate props
props.product.name = 'New Name';  // BAD

// Don't use long if-else chains
if (x === 1) { ... } else if (x === 2) { ... } else if (x === 3) { ... }  // BAD

// Don't inline complex logic in templates
<div v-if="items.filter(i => i.active).map(i => i.id).includes(currentId)">  // BAD

// Don't use magic numbers
if (status === 3) { ... }  // BAD - use constants/enums
```

### Composable Guidelines

Extract to composables when:

- Logic is used in 2+ components
- Logic is complex (>20 lines)
- Logic involves side effects (API calls, localStorage)

```typescript
// src/composables/useProductPrice.ts
export function useProductPrice(product: Ref<Product>) {
  const basePrice = computed(() => product.value.base_price);

  const currentPrice = computed(
    () => product.value.sale_price ?? product.value.base_price
  );

  const discountPercentage = computed(() => {
    if (!product.value.sale_price) return 0;
    return Math.round(
      (1 - product.value.sale_price / product.value.base_price) * 100
    );
  });

  const formatPrice = (price: number) => `₪${price.toFixed(2)}`;

  return {
    basePrice,
    currentPrice,
    discountPercentage,
    formatPrice,
  };
}
```

---

## Required Skills

**IMPORTANT:** Before working on this project, invoke these skills:

1. **Quasar Vue3 Skill** - For all Quasar Framework related work
2. **Supabase Skill** - For authentication and database operations

```
// At the start of each session:
Skill: quasar-vue3
Skill: supabase
```

---

## UI Development Workflow

### Step 1: Design with Stitch (Google)

Use [Stitch](https://stitch.google.com) to generate initial UI designs. Stitch outputs React + Tailwind HTML templates.

### Step 2: Convert to Quasar Native

**MANDATORY:** Convert ALL Stitch output to Quasar native components and classes.

#### Conversion Rules:

| Stitch/Tailwind      | Quasar Equivalent                               |
| -------------------- | ----------------------------------------------- |
| `<button>`           | `<q-btn>`                                       |
| `<input>`            | `<q-input>`                                     |
| `<select>`           | `<q-select>`                                    |
| `<div class="flex">` | `<div class="row">` or `<div class="flex">`     |
| `<div class="grid">` | `<div class="row q-col-gutter-md">`             |
| `p-4`                | `q-pa-md`                                       |
| `m-2`                | `q-ma-sm`                                       |
| `text-lg`            | `text-h6` or `text-body1`                       |
| `bg-blue-500`        | `bg-primary`                                    |
| `rounded-lg`         | `rounded-borders`                               |
| `shadow-md`          | `shadow-2`                                      |
| `hover:`             | Use Quasar's `:class` bindings or `q-hoverable` |

### Step 3: CSS Guidelines

**DO:**

```vue
<!-- Use Quasar utility classes -->
<div class="q-pa-md q-mb-lg">
<q-btn color="primary" class="full-width q-mt-md">
<div class="row q-col-gutter-md">
<div class="col-12 col-md-6">
```

**DON'T:**

```vue
<!-- Never use Tailwind classes -->
<div class="p-4 mb-8">
<button class="w-full mt-4 bg-blue-500">
<div class="grid grid-cols-2 gap-4">
```

### Step 4: Component Usage

Always use Quasar components:

```vue
<!-- CORRECT -->
<q-card class="q-pa-md">
  <q-card-section>
    <q-input v-model="email" :label="$t('auth.email')" />
  </q-card-section>
  <q-card-actions>
    <q-btn color="primary" :label="$t('common.submit')" />
  </q-card-actions>
</q-card>

<!-- INCORRECT -->
<div class="bg-white shadow-lg rounded-lg p-4">
  <input type="email" class="border rounded p-2" />
  <button class="bg-blue-500 text-white px-4 py-2">Submit</button>
</div>
```

---

## Translation Guidelines

### All Text MUST Be Translated

**NEVER hardcode text. Always use i18n:**

```vue
<!-- CORRECT -->
<q-btn :label="$t('products.addToCart')" />
<p>{{ $t('cart.empty') }}</p>
<q-input :label="$t('auth.email')" />

<!-- INCORRECT -->
<q-btn label="Add to Cart" />
<p>Your cart is empty</p>
<q-input label="Email" />
```

### Translation File Structure

All translations must be aligned between English and Hebrew:

```typescript
// src/i18n/en-US/index.ts
export default {
  products: {
    addToCart: "Add to Cart",
    buyNow: "Buy Now",
  },
};

// src/i18n/he/index.ts
export default {
  products: {
    addToCart: "הוסף לעגלה",
    buyNow: "קנה עכשיו",
  },
};
```

### Adding New Translations

When adding any new text:

1. Add to BOTH `en-US/index.ts` AND `he/index.ts`
2. Use the same key structure
3. Group by feature/page

```typescript
// Adding new feature translations
// Step 1: Add to en-US
wishlist: {
  title: 'My Wishlist',
  addToWishlist: 'Add to Wishlist',
  removeFromWishlist: 'Remove from Wishlist',
  empty: 'Your wishlist is empty',
}

// Step 2: Add SAME keys to he
wishlist: {
  title: 'רשימת המשאלות שלי',
  addToWishlist: 'הוסף לרשימת משאלות',
  removeFromWishlist: 'הסר מרשימת משאלות',
  empty: 'רשימת המשאלות ריקה',
}
```

---

## Quasar Utility Classes Reference

### Spacing

- `q-pa-{size}` - padding all (none, xs, sm, md, lg, xl)
- `q-ma-{size}` - margin all
- `q-pt-{size}` - padding top
- `q-mb-{size}` - margin bottom
- etc.

### Typography

- `text-h1` through `text-h6` - headings
- `text-subtitle1`, `text-subtitle2` - subtitles
- `text-body1`, `text-body2` - body text
- `text-caption`, `text-overline` - small text
- `text-weight-bold`, `text-weight-medium`
- `text-center`, `text-left`, `text-right`

### Colors

- `text-primary`, `text-secondary`, `text-accent`
- `bg-primary`, `bg-secondary`, `bg-dark`
- `text-positive`, `text-negative`, `text-warning`, `text-info`

### Layout

- `row`, `column` - flex containers
- `col`, `col-auto`, `col-{1-12}` - grid columns
- `col-md-{n}`, `col-lg-{n}` - responsive columns
- `q-col-gutter-{size}` - column gaps
- `justify-center`, `justify-between`, `items-center`
- `full-width`, `full-height`

### Display

- `flex`, `inline-flex`, `block`, `inline-block`
- `hidden`, `invisible`
- `gt-xs`, `lt-md` - responsive visibility

### Borders & Shadows

- `rounded-borders` - border radius
- `no-border`, `no-border-radius`
- `shadow-1` through `shadow-24`

---

## RTL Considerations

### Always Test Both Directions

```vue
<template>
  <!-- Layout automatically flips in RTL -->
  <div class="row">
    <div class="col-12 col-md-8">Main content</div>
    <div class="col-12 col-md-4">Sidebar</div>
  </div>
</template>
```

## File Naming Conventions

- Pages: `IndexPage.vue`, `ProductPage.vue`
- Components: `ProductCard.vue`, `CartDrawer.vue`
- Composables: `useAuth.ts`, `useCart.ts`
- Stores: `auth.store.ts`, `cart.store.ts`
- Services: `strapi.service.ts`, `cloudinary.service.ts`
- Types: `product.ts`, `order.ts`

---

## Checklist Before Committing

- [ ] All text uses `$t()` translations
- [ ] Hebrew translations added for all new text
- [ ] No Tailwind classes used
- [ ] Only Quasar native components used.
- [ ] No inline css. No customm css unless no other choice
- [ ] Mobile responsive
- [ ] No console errors
- [ ] TypeScript compiles without errors
- [ ] No ESLINT errors
