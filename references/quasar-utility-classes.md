# Quasar Utility Classes Reference

Complete mapping of CSS properties to Quasar utility classes for the component-scanner agent.

## Spacing

Quasar uses a spacing scale: `none`=0, `xs`=4px, `sm`=8px, `md`=16px, `lg`=24px, `xl`=48px

### Padding

| CSS Property | CSS Value | Quasar Class |
|--------------|-----------|--------------|
| `padding` | 0 | `q-pa-none` |
| `padding` | 4px | `q-pa-xs` |
| `padding` | 8px | `q-pa-sm` |
| `padding` | 16px | `q-pa-md` |
| `padding` | 24px | `q-pa-lg` |
| `padding` | 48px | `q-pa-xl` |
| `padding-top` | 0/4/8/16/24/48px | `q-pt-none/xs/sm/md/lg/xl` |
| `padding-right` | 0/4/8/16/24/48px | `q-pr-none/xs/sm/md/lg/xl` |
| `padding-bottom` | 0/4/8/16/24/48px | `q-pb-none/xs/sm/md/lg/xl` |
| `padding-left` | 0/4/8/16/24/48px | `q-pl-none/xs/sm/md/lg/xl` |
| `padding-left` + `padding-right` | same | `q-px-none/xs/sm/md/lg/xl` |
| `padding-top` + `padding-bottom` | same | `q-py-none/xs/sm/md/lg/xl` |

### Margin

| CSS Property | CSS Value | Quasar Class |
|--------------|-----------|--------------|
| `margin` | 0 | `q-ma-none` |
| `margin` | 4px | `q-ma-xs` |
| `margin` | 8px | `q-ma-sm` |
| `margin` | 16px | `q-ma-md` |
| `margin` | 24px | `q-ma-lg` |
| `margin` | 48px | `q-ma-xl` |
| `margin` | auto | `q-ma-auto` |
| `margin-top` | 0/4/8/16/24/48px/auto | `q-mt-none/xs/sm/md/lg/xl/auto` |
| `margin-right` | 0/4/8/16/24/48px/auto | `q-mr-none/xs/sm/md/lg/xl/auto` |
| `margin-bottom` | 0/4/8/16/24/48px/auto | `q-mb-none/xs/sm/md/lg/xl/auto` |
| `margin-left` | 0/4/8/16/24/48px/auto | `q-ml-none/xs/sm/md/lg/xl/auto` |
| `margin-left` + `margin-right` | same | `q-mx-none/xs/sm/md/lg/xl/auto` |
| `margin-top` + `margin-bottom` | same | `q-my-none/xs/sm/md/lg/xl/auto` |

---

## Flexbox

### Container

| CSS | Quasar Class |
|-----|--------------|
| `display: flex` | `flex` |
| `display: flex; flex-direction: row` | `row` |
| `display: flex; flex-direction: column` | `column` |
| `display: flex; flex-direction: row-reverse` | `row reverse` |
| `display: flex; flex-direction: column-reverse` | `column reverse` |
| `display: inline-flex` | `inline` (combine with row/column) |

### Justify Content (main axis)

| CSS | Quasar Class |
|-----|--------------|
| `justify-content: flex-start` | `justify-start` |
| `justify-content: flex-end` | `justify-end` |
| `justify-content: center` | `justify-center` |
| `justify-content: space-between` | `justify-between` |
| `justify-content: space-around` | `justify-around` |
| `justify-content: space-evenly` | `justify-evenly` |

### Align Items (cross axis)

| CSS | Quasar Class |
|-----|--------------|
| `align-items: flex-start` | `items-start` |
| `align-items: flex-end` | `items-end` |
| `align-items: center` | `items-center` |
| `align-items: baseline` | `items-baseline` |
| `align-items: stretch` | `items-stretch` |

### Align Self (individual item)

| CSS | Quasar Class |
|-----|--------------|
| `align-self: flex-start` | `self-start` |
| `align-self: flex-end` | `self-end` |
| `align-self: center` | `self-center` |
| `align-self: baseline` | `self-baseline` |
| `align-self: stretch` | `self-stretch` |

### Align Content (multi-line)

| CSS | Quasar Class |
|-----|--------------|
| `align-content: flex-start` | `content-start` |
| `align-content: flex-end` | `content-end` |
| `align-content: center` | `content-center` |
| `align-content: stretch` | `content-stretch` |
| `align-content: space-between` | `content-between` |
| `align-content: space-around` | `content-around` |

### Flex Wrap

| CSS | Quasar Class |
|-----|--------------|
| `flex-wrap: wrap` | `wrap` |
| `flex-wrap: nowrap` | `no-wrap` |
| `flex-wrap: wrap-reverse` | `reverse-wrap` |

### Flex Order

| CSS | Quasar Class |
|-----|--------------|
| `order: -1` | `order-first` |
| `order: 1` (last) | `order-last` |
| `order: 0` | `order-none` |

### Flex Grow/Shrink

| CSS | Quasar Class |
|-----|--------------|
| `flex: 1 1 0%` (grow) | `col-grow` |
| `flex: 0 0 auto` (no grow) | `col-shrink` |
| `flex: 1 1 auto` (auto) | `col-auto` |

### Gap/Gutter

| CSS | Quasar Class |
|-----|--------------|
| `gap: 4px` | `q-gutter-xs` |
| `gap: 8px` | `q-gutter-sm` |
| `gap: 16px` | `q-gutter-md` |
| `gap: 24px` | `q-gutter-lg` |
| `gap: 48px` | `q-gutter-xl` |
| `column-gap: *` | `q-gutter-x-*` |
| `row-gap: *` | `q-gutter-y-*` |
| Grid column gutter | `q-col-gutter-*` |

---

## Typography

### Text Size (Headings)

| CSS Equivalent | Quasar Class |
|----------------|--------------|
| font-size: 6rem, weight: 300, letter-spacing: -0.01562em | `text-h1` |
| font-size: 3.75rem, weight: 300, letter-spacing: -0.00833em | `text-h2` |
| font-size: 3rem, weight: 400, letter-spacing: normal | `text-h3` |
| font-size: 2.125rem, weight: 400, letter-spacing: 0.00735em | `text-h4` |
| font-size: 1.5rem, weight: 400, letter-spacing: normal | `text-h5` |
| font-size: 1.25rem, weight: 500, letter-spacing: 0.0125em | `text-h6` |
| font-size: 1rem, weight: 400, letter-spacing: 0.00937em | `text-subtitle1` |
| font-size: 0.875rem, weight: 500, letter-spacing: 0.00714em | `text-subtitle2` |
| font-size: 1rem, weight: 400, letter-spacing: 0.03125em | `text-body1` |
| font-size: 0.875rem, weight: 400, letter-spacing: 0.01786em | `text-body2` |
| font-size: 0.75rem, weight: 400, letter-spacing: 0.03333em | `text-caption` |
| font-size: 0.75rem, weight: 500, letter-spacing: 0.16667em, uppercase | `text-overline` |

### Text Alignment

| CSS | Quasar Class |
|-----|--------------|
| `text-align: left` | `text-left` |
| `text-align: center` | `text-center` |
| `text-align: right` | `text-right` |
| `text-align: justify` | `text-justify` |

### Font Weight

| CSS | Quasar Class |
|-----|--------------|
| `font-weight: 100` | `text-weight-thin` |
| `font-weight: 300` | `text-weight-light` |
| `font-weight: 400` | `text-weight-regular` |
| `font-weight: 500` | `text-weight-medium` |
| `font-weight: 700` or `bold` | `text-weight-bold` or `text-bold` |
| `font-weight: 900` | `text-weight-bolder` |

### Font Style

| CSS | Quasar Class |
|-----|--------------|
| `font-style: italic` | `text-italic` |

### Text Transform

| CSS | Quasar Class |
|-----|--------------|
| `text-transform: uppercase` | `text-uppercase` |
| `text-transform: lowercase` | `text-lowercase` |
| `text-transform: capitalize` | `text-capitalize` |

### Text Decoration

| CSS | Quasar Class |
|-----|--------------|
| `text-decoration: line-through` | `text-strike` |
| `text-decoration: underline` | (use native CSS) |

### White Space / Overflow

| CSS | Quasar Class |
|-----|--------------|
| `white-space: nowrap` | `text-no-wrap` |
| `text-overflow: ellipsis; overflow: hidden; white-space: nowrap` | `ellipsis` |
| 2-line ellipsis | `ellipsis-2-lines` |
| 3-line ellipsis | `ellipsis-3-lines` |

---

## Colors

### Text Colors

| Color | Quasar Class |
|-------|--------------|
| Primary (typically #1976D2) | `text-primary` |
| Secondary (typically #26A69A) | `text-secondary` |
| Accent (typically #9C27B0) | `text-accent` |
| Positive/Success (green) | `text-positive` |
| Negative/Error (red) | `text-negative` |
| Info (cyan) | `text-info` |
| Warning (orange) | `text-warning` |
| Dark | `text-dark` |
| White | `text-white` |
| Black | `text-black` |
| Grey | `text-grey` |

### Background Colors

| Color | Quasar Class |
|-------|--------------|
| Primary | `bg-primary` |
| Secondary | `bg-secondary` |
| Accent | `bg-accent` |
| Positive | `bg-positive` |
| Negative | `bg-negative` |
| Info | `bg-info` |
| Warning | `bg-warning` |
| Dark | `bg-dark` |
| White | `bg-white` |
| Black | `bg-black` |
| Grey | `bg-grey` |
| Transparent | `bg-transparent` |

### Material Colors (text-* and bg-*)

Available colors with shades 1-14:
- `red`, `pink`, `purple`, `deep-purple`
- `indigo`, `blue`, `light-blue`, `cyan`
- `teal`, `green`, `light-green`, `lime`
- `yellow`, `amber`, `orange`, `deep-orange`
- `brown`, `grey`, `blue-grey`

Example: `text-red-8`, `bg-blue-3`, `text-deep-purple-14`

---

## Sizing

| CSS | Quasar Class |
|-----|--------------|
| `width: 100%; height: 100%` | `fit` |
| `width: 100%` | `full-width` |
| `height: 100%` | `full-height` |
| `max-width: 100%` | `max-width-100` |
| `height: 100vh` | `window-height` |
| `min-height: 100vh` | `window-height` |
| `width: 100vw` | `window-width` |

---

## Display

| CSS | Quasar Class |
|-----|--------------|
| `display: block` | `block` |
| `display: inline-block` | `inline-block` |
| `display: none` | `hidden` |
| `visibility: hidden` | `invisible` |

---

## Shadows (Elevation)

Material Design elevation shadows:

| Elevation | Quasar Class |
|-----------|--------------|
| Level 1 | `shadow-1` |
| Level 2 | `shadow-2` |
| Level 3 | `shadow-3` |
| Level 4 | `shadow-4` |
| Level 5 | `shadow-5` |
| Level 6 | `shadow-6` |
| Level 7 | `shadow-7` |
| Level 8 | `shadow-8` |
| Level 9 | `shadow-9` |
| Level 10 | `shadow-10` |
| Level 11-24 | `shadow-11` through `shadow-24` |
| No shadow | `no-shadow` |
| Upward shadows | `shadow-up-1` through `shadow-up-24` |
| Inset shadow | `inset-shadow` |
| Inset shadow down | `inset-shadow-down` |

---

## Positioning

| CSS | Quasar Class |
|-----|--------------|
| `position: relative` | `relative-position` |
| `position: absolute` | `absolute` |
| `position: fixed` | `fixed` |
| `position: absolute; top: 0; left: 0; right: 0; bottom: 0` | `absolute-full` |
| `position: absolute` + centered | `absolute-center` |
| `position: absolute; top: 0` | `absolute-top` |
| `position: absolute; bottom: 0` | `absolute-bottom` |
| `position: absolute; left: 0` | `absolute-left` |
| `position: absolute; right: 0` | `absolute-right` |
| `position: absolute; top: 0; left: 0` | `absolute-top-left` |
| `position: absolute; top: 0; right: 0` | `absolute-top-right` |
| `position: absolute; bottom: 0; left: 0` | `absolute-bottom-left` |
| `position: absolute; bottom: 0; right: 0` | `absolute-bottom-right` |
| `position: fixed; top: 0; left: 0; right: 0; bottom: 0` | `fixed-full` |
| `position: fixed` + centered | `fixed-center` |
| Fixed edges | `fixed-top`, `fixed-bottom`, `fixed-left`, `fixed-right` |
| Fullscreen | `fullscreen` |

---

## Border & Border Radius

| CSS | Quasar Class |
|-----|--------------|
| `border-radius: $generic-border-radius` (4px) | `rounded-borders` |
| `border-radius: inherit` | `border-radius-inherit` |
| `border-radius: 0` | `no-border-radius` |
| `border: none` | `no-border` |

---

## Overflow

| CSS | Quasar Class |
|-----|--------------|
| `overflow: hidden` | `overflow-hidden` |
| `overflow-y: hidden` | `overflow-hidden-y` |
| `overflow: auto` | `overflow-auto` |
| Hide scrollbar | `hide-scrollbar` |

---

## Float

| CSS | Quasar Class |
|-----|--------------|
| `float: left` | `float-left` |
| `float: right` | `float-right` |

---

## Vertical Align

| CSS | Quasar Class |
|-----|--------------|
| `vertical-align: top` | `vertical-top` |
| `vertical-align: middle` | `vertical-middle` |
| `vertical-align: bottom` | `vertical-bottom` |

---

## Cursor

| CSS | Quasar Class |
|-----|--------------|
| `cursor: pointer` (with hover effect) | `q-hoverable cursor-pointer` |
| `cursor: not-allowed` (disabled state) | `disabled` |
| `pointer-events: none` | `no-pointer-events` |

---

## Miscellaneous

| CSS | Quasar Class |
|-----|--------------|
| `margin: 0` | `no-margin` |
| `padding: 0` | `no-padding` |
| `box-shadow: none` | `no-box-shadow` or `no-shadow` |
| `outline: none` | `no-outline` |
| `background: transparent` | `transparent` |
| Glossy gradient effect | `glossy` |
| `transition: none` | `no-transition` |
| `transition-duration: 0` | `transition-0` |
| Dimmed overlay effect | `dimmed` |
| Light dimmed effect | `light-dimmed` |

---

## Responsive Variants

Most utility classes support responsive breakpoint suffixes:
- `-xs` - Extra small (< 600px)
- `-sm` - Small (600px - 1023px)
- `-md` - Medium (1024px - 1439px)
- `-lg` - Large (1440px - 1919px)
- `-xl` - Extra large (>= 1920px)

Example: `q-pa-md-lg` applies `q-pa-lg` on medium screens and above.

---

## Grid System (12-column)

| CSS Equivalent | Quasar Class |
|----------------|--------------|
| Auto width column | `col-auto` |
| Equal width column | `col` |
| 1/12 width | `col-1` |
| 2/12 width | `col-2` |
| ... | ... |
| 12/12 width | `col-12` |
| Offset by columns | `offset-1` through `offset-11` |

Responsive: `col-xs-*`, `col-sm-*`, `col-md-*`, `col-lg-*`, `col-xl-*`
