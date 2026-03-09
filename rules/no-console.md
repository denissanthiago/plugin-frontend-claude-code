---
name: no-console
description: Do not leave console.log or debug statements in production code
globs: "*.ts,*.tsx,*.js,*.jsx"
---

## No Console in Production

Never leave `console.log`, `console.debug`, `console.info`, or `console.warn` in production code.

### Forbidden

```tsx
console.log('user data:', user)
console.debug('rendering component')
console.info('fetching data')
console.warn('deprecated usage')
```

### Allowed

**`console.error`** is allowed for actual error handling:

```tsx
try {
  await submitForm(data)
} catch (error) {
  console.error('Form submission failed:', error)
}
```

**Logging services** — use a proper logger instead:

```tsx
import { logger } from '@/lib/logger'

logger.info('User logged in', { userId })
logger.error('Payment failed', { orderId, error })
```

### During development

If you need debug logging during development, use a pattern that gets stripped in production:

```tsx
if (process.env.NODE_ENV === 'development') {
  console.log('debug:', data)
}
```

Or remove it entirely before committing.
