---
name: quasar-vue3
description: Comprehensive Quasar Framework (v2) and Vue 3 development assistance. Use this skill when working with Quasar projects, components, plugins, directives, composables, CLI configuration, or building apps (SPA, SSR, PWA, Electron, Capacitor, Cordova, Browser Extensions). Triggers on Quasar-specific questions, quasar.config.js, Q-prefixed components (QBtn, QInput, QTable, etc.), Quasar CLI commands, or Vue 3 Composition API with Quasar.
---

# Quasar Vue3 Development

Quasar is a Vue 3 framework for building responsive SPAs, SSR apps, PWAs, mobile apps (Capacitor/Cordova), desktop apps (Electron), and browser extensions from a single codebase.

## Reference Documentation

All Quasar documentation is in `references/`. Use grep patterns to find relevant docs.

### Quick Reference Index

| Topic | Location | Grep Pattern |
|-------|----------|--------------|
| **Commands** | `commands/` | `refactor` |
| **Agents** | `agents/` | `component-scanner` |
| Components | `references/vue-components/` | `QBtn\|QInput\|QTable\|QCard` |
| Directives | `references/vue-directives/` | `v-ripple\|v-close-popup\|v-touch` |
| Composables | `references/vue-composables/` | `useQuasar\|useMeta\|useDialog` |
| Plugins | `references/quasar-plugins/` | `Notify\|Dialog\|Loading\|Dark` |
| Utilities | `references/quasar-utils/` | `date-utils\|color-utils\|dom-utils` |
| CLI (Vite) | `references/quasar-cli-vite/` | `quasar.config\|boot-files\|routing` |
| CLI (Webpack) | `references/quasar-cli-webpack/` | Same as Vite |
| Layout | `references/layout/` | `QLayout\|QDrawer\|QHeader\|grid` |
| Styling | `references/style/` | `sass-scss\|color-palette\|dark-mode` |
| Options | `references/options/` | `platform-detection\|screen-plugin\|i18n` |

### Build Modes

- **SPA**: `references/quasar-cli-vite/developing-spa/`
- **SSR**: `references/quasar-cli-vite/developing-ssr/`
- **PWA**: `references/quasar-cli-vite/developing-pwa/`
- **Electron**: `references/quasar-cli-vite/developing-electron-apps/`
- **Capacitor**: `references/quasar-cli-vite/developing-capacitor-apps/`
- **Cordova**: `references/quasar-cli-vite/developing-cordova-apps/`
- **BEX**: `references/quasar-cli-vite/developing-browser-extensions/`

## Common Patterns

### Component Usage
```vue
<template>
  <q-btn color="primary" label="Click" @click="onClick" />
  <q-input v-model="text" label="Enter text" />
</template>

<script setup>
import { ref } from 'vue'
import { useQuasar } from 'quasar'

const $q = useQuasar()
const text = ref('')

const onClick = () => {
  $q.notify('Clicked!')
}
</script>
```

### Plugin Usage (Notify, Dialog, Loading)
```js
import { useQuasar } from 'quasar'

const $q = useQuasar()

// Notify
$q.notify({ message: 'Success', color: 'positive' })

// Dialog
$q.dialog({ title: 'Confirm', message: 'Are you sure?' })
  .onOk(() => { /* confirmed */ })

// Loading
$q.loading.show()
$q.loading.hide()
```

### Boot Files (quasar.config.js)
```js
// quasar.config.js
boot: ['axios', 'i18n']

// src/boot/axios.js
import { boot } from 'quasar/wrappers'
import axios from 'axios'

export default boot(({ app }) => {
  app.config.globalProperties.$axios = axios
})
```

## Finding Documentation

1. **Component API**: Read `references/vue-components/{component}.md`
2. **Directive usage**: Read `references/vue-directives/{directive}.md`
3. **Configuration**: Read `references/quasar-cli-vite/quasar-config-file.md`
4. **Build mode setup**: Read intro file in respective `developing-{mode}/` folder
5. **Styling/theming**: Read `references/style/` files

## Available Agents

### Component Scanner

Scans Vue/Quasar components for code quality improvements. The agent performs four checks:

1. **CSS Utility Classes** - Finds custom CSS that could use Quasar utility classes
2. **Linting & TypeScript** - Runs ESLint and type checking
3. **Component Structure** - Checks size metrics and suggests splitting
4. **Translation Check** - Finds hardcoded strings needing i18n

**Usage examples:**
- "Scan my UserProfile.vue component"
- "Check if I can use Quasar utility classes instead of custom CSS"
- "Is this component too large? Should I split it?"
- "Find untranslated strings in my components"

**Configuration flags:**
- `--i18n=vue-i18n|quasar|both` - Translation pattern to check
- `--skip-lint` - Skip ESLint/TypeScript check
- `--skip-css` - Skip CSS utility check
- `--skip-structure` - Skip structure analysis
- `--skip-translation` - Skip translation check

**Reference:** See `references/quasar-utility-classes.md` for complete CSS-to-class mappings.

## Slash Commands

### /refactor [path]

Scans Vue/Quasar components and offers to fix issues found.

**Usage:**
- `/refactor` - Scan current file or prompt for path
- `/refactor src/components/UserProfile.vue` - Scan specific file
- `/refactor src/components/` - Scan all components in directory

**What it checks:**
1. CSS that could use Quasar utility classes
2. ESLint and TypeScript errors
3. Component size and structure
4. Hardcoded strings needing translation

**Behavior:** After scanning, you'll be asked if you want to fix the issues found.

## Key Files in Quasar Projects

```
project/
├── quasar.config.js      # Main config (build, plugins, framework)
├── src/
│   ├── boot/             # Boot files (init code)
│   ├── components/       # Vue components
│   ├── layouts/          # Layout components
│   ├── pages/            # Route pages
│   ├── router/           # Vue Router config
│   ├── stores/           # Pinia stores
│   ├── css/              # Global styles, Quasar variables
│   └── App.vue           # Root component
```
