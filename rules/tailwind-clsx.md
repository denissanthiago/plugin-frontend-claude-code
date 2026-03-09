---
name: tailwind-clsx
description: Always use Tailwind CSS for styling and clsx for conditional classes
globs: "*.tsx,*.jsx,*.ts,*.js"
---

## Styling Rules

### Always use Tailwind CSS
- Use Tailwind utility classes for all styling. Never use inline styles (`style={{}}`), CSS modules, or styled-components.
- Use the project's design tokens via Tailwind theme (`text-primary`, `bg-background`, etc.) instead of arbitrary values (`text-[#ff0000]`).

### Always use clsx for conditional classes
- Use `clsx` for any conditional or dynamic class composition. Never use template literals or string concatenation for classes.

**Correct:**
```tsx
import clsx from 'clsx'

<div className={clsx('p-4 rounded-lg', isActive && 'bg-blue-500 text-white', isDisabled && 'opacity-50 cursor-not-allowed')} />
```

**Wrong:**
```tsx
// Never do this
<div className={`p-4 rounded-lg ${isActive ? 'bg-blue-500 text-white' : ''}`} />
<div className={'p-4 rounded-lg ' + (isActive ? 'bg-blue-500' : '')} />
<div style={{ padding: '16px', borderRadius: '8px' }} />
```

### clsx patterns

**Boolean conditions:**
```tsx
clsx('base-class', condition && 'conditional-class')
```

**Object syntax:**
```tsx
clsx('base-class', {
  'bg-blue-500': isActive,
  'bg-gray-200': !isActive,
  'opacity-50': isDisabled,
})
```

**With CVA variants:**
```tsx
import { cva } from 'class-variance-authority'
import clsx from 'clsx'

const button = cva('px-4 py-2 rounded font-medium', {
  variants: {
    variant: {
      primary: 'bg-blue-500 text-white',
      secondary: 'bg-gray-200 text-gray-800',
    },
  },
})

<button className={clsx(button({ variant: 'primary' }), className)} />
```
