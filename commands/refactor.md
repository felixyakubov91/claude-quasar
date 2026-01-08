---
name: refactor
description: Scan and refactor Vue/Quasar component(s) - checks CSS utilities, linting, structure, and translations
arguments:
  - name: path
    description: Path to component file or directory (optional)
---

# Component Refactor

Scan the specified Vue/Quasar component(s) for code quality improvements.

**Target:** $ARGUMENTS

If no path is specified, ask the user which file(s) to scan or look for `.vue` files in the current directory.

## Checks to Perform

### 1. CSS Utility Class Opportunities

Analyze the `<style>` section and inline styles for CSS that could be replaced with Quasar utility classes:

| CSS Pattern | Quasar Class |
|-------------|--------------|
| `padding: 0/4px/8px/16px/24px/48px` | `q-pa-none/xs/sm/md/lg/xl` |
| `margin: ...` | `q-ma-*`, `q-mt-*`, `q-mb-*`, etc. |
| `display: flex` | `flex`, `row`, `column` |
| `justify-content: center` | `justify-center` |
| `align-items: center` | `items-center` |
| `text-align: center` | `text-center` |
| `font-weight: bold/700` | `text-bold` |
| `width: 100%` | `full-width` |
| `height: 100%` | `full-height` |
| `box-shadow: ...` | `shadow-1` through `shadow-24` |

Reference `references/quasar-utility-classes.md` for the complete mapping.

### 2. Linting & TypeScript

Run ESLint and TypeScript checks:
```bash
npx eslint --format stylish <file>
npx vue-tsc --noEmit 2>&1 | grep -A2 "<file>"
```

Report any errors or warnings with line numbers.

### 3. Component Structure

Check these metrics against thresholds:

| Metric | Warning | Error |
|--------|---------|-------|
| Template lines | >150 | >300 |
| Script lines | >200 | >400 |
| Style lines | >100 | >200 |
| Props count | >10 | >20 |
| Emits count | >8 | >15 |
| Template nesting depth | >6 | >10 |

If thresholds exceeded, suggest:
- Extracting child components
- Creating composables for reusable logic
- Splitting by feature/concern

### 4. Translation Check

Find hardcoded strings that should use i18n:

**Check these locations:**
- Text content between tags: `<div>Hello</div>`
- Translatable attributes: `label`, `title`, `placeholder`, `hint`, `message`, `caption`
- Strings in `$q.notify()`, `$q.dialog()` calls

**Ignore:**
- CSS classes, event names, component names
- URLs, paths, technical identifiers
- Numbers, single characters

**Support both patterns:**
- vue-i18n: `$t('key')`, `t('key')`, `useI18n()`
- Quasar Lang: `$q.lang.*`, `useQuasar().lang`

## Output Format

Generate a structured report:

```markdown
# Scan Report: [filename]

## Summary
| Category | Issues |
|----------|--------|
| CSS Utilities | X opportunities |
| Linting | X errors, Y warnings |
| Structure | X warnings |
| Translations | X strings |

## Details
[Details for each category with line numbers and suggestions]
```

## After Scanning

If issues are found:

1. Present the report to the user
2. Ask: **"Would you like me to help fix these issues?"**
3. Wait for user response
4. If user confirms, offer to fix issues one category at a time:
   - "Fix CSS utility opportunities?"
   - "Address linting issues?"
   - "Help restructure component?"
   - "Add translation keys?"

Do NOT make any changes without explicit user confirmation.
