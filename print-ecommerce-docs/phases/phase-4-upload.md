# Phase 4: Image Upload & Editor

## Overview
Build the advanced image upload and manipulation system using Cloudinary.

## Duration
Days 11-15

## Goals
- Integrate Cloudinary upload widget
- Build advanced image editor (crop, rotate, filters, text)
- Create product mockup preview
- Save transformations to Strapi
- Set up Vultr Object Storage for archival

## Tasks
| Task | File | Description |
|------|------|-------------|
| 4.1 | `tasks/4.1-cloudinary-upload.md` | Cloudinary upload widget integration |
| 4.2 | `tasks/4.2-image-editor.md` | Advanced image editor component |
| 4.3 | `tasks/4.3-product-mockup.md` | Preview image on product template |
| 4.4 | `tasks/4.4-save-transformations.md` | Save edited images to Strapi |
| 4.5 | `tasks/4.5-vultr-storage.md` | Vultr Object Storage archival |

## Prerequisites
- Phase 3 completed
- Cloudinary account with API credentials
- Vultr Object Storage bucket created

## Image Editor Features

### Basic Tools
- **Crop**: Free-form and preset aspect ratios (product dimensions)
- **Rotate**: 90° increments + free rotation
- **Flip**: Horizontal and vertical

### Advanced Tools
- **Brightness/Contrast**: -100 to +100 range
- **Saturation**: -100 to +100 range
- **Filters**: Preset filters (grayscale, sepia, vintage, etc.)
- **Text Overlay**: Add text with font, size, color options
- **Background Removal**: Cloudinary AI-powered

### Print-Specific
- **DPI Indicator**: Show if image meets print quality
- **Bleed Area**: Visual guide for print margins
- **Safe Zone**: Visual guide for content area

## Upload Flow

```
┌─────────────────┐
│  User selects   │
│  file(s)        │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Cloudinary     │
│  Upload Widget  │
│  (signed)       │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Progress       │
│  tracking       │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Image Editor   │──────┐
│  opens          │      │
└────────┬────────┘      │
         │               │ User edits
         ▼               │
┌─────────────────┐      │
│  Apply          │◄─────┘
│  transformations│
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Save to Strapi │
│  (UploadedImage)│
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Archive to     │
│  Vultr Storage  │
└─────────────────┘
```

## Cloudinary Transformations

```typescript
// Basic transformations
{
  crop: 'fill',
  width: 1000,
  height: 1000,
  gravity: 'auto',
  quality: 'auto:best',
  format: 'auto'
}

// With effects
{
  effect: 'grayscale',
  effect: 'brightness:20',
  effect: 'contrast:30'
}

// Text overlay
{
  overlay: {
    font_family: 'Arial',
    font_size: 48,
    text: 'Hello World'
  },
  gravity: 'center',
  color: '#ffffff'
}

// Background removal
{
  effect: 'background_removal'
}
```

## Key Components

### ImageUploader.vue
- QUploader with Cloudinary factory
- Multiple file support
- Progress indicators
- Drag and drop zone
- File type validation (jpg, png, pdf, tiff)
- Max file size: 50MB

### ImageEditor.vue
- Canvas-based editing
- Tool palette (left sidebar)
- Preview area (center)
- Properties panel (right sidebar)
- Undo/redo support
- Save/cancel buttons

### ProductMockup.vue
- Load product template image
- Overlay user image in designated area
- Real-time preview during editing
- Multiple views if product has them

## Files Created After Phase 4
```
frontend/src/
├── boot/
│   └── cloudinary.ts
├── services/
│   └── cloudinary.service.ts
├── pages/
│   └── upload/
│       ├── IndexPage.vue
│       └── EditorPage.vue
├── components/
│   └── upload/
│       ├── ImageUploader.vue
│       ├── ImageEditor.vue
│       ├── EditorToolbar.vue
│       ├── EditorCanvas.vue
│       ├── ProductMockup.vue
│       └── UploadProgress.vue
├── composables/
│   └── useUpload.ts
└── types/
    └── upload.ts
```

## Acceptance Criteria
- [ ] Files upload to Cloudinary successfully
- [ ] Upload progress shows correctly
- [ ] Image editor opens after upload
- [ ] Crop tool works with aspect ratio lock
- [ ] Rotate and flip work correctly
- [ ] Brightness/contrast adjustments work
- [ ] Text overlay can be added
- [ ] Background removal works (Cloudinary AI)
- [ ] Product mockup shows image correctly
- [ ] Transformations save to Strapi
- [ ] Original files archive to Vultr
- [ ] Works on mobile (touch gestures)
