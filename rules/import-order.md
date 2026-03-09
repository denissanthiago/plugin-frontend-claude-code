---
name: import-order
description: Enforce consistent import ordering with grouped sections
globs: "*.ts,*.tsx,*.js,*.jsx"
---

## Import Order

Imports must follow this order, separated by blank lines between groups:

```tsx
// 1. React
import { useState, useEffect } from 'react'

// 2. Next.js
import { useRouter } from 'next/navigation'
import Image from 'next/image'

// 3. Third-party libraries
import { useQuery } from '@tanstack/react-query'
import { useForm } from 'react-hook-form'
import clsx from 'clsx'

// 4. Components
import { Button } from '@/components/atoms/button'
import { UserCard } from '@/components/molecules/user-card'

// 5. Hooks
import { useAuth } from '@/hooks/use-auth'
import { useDebounce } from '@/hooks/use-debounce'

// 6. Utils and helpers
import { formatDate } from '@/utils/format-date'
import { cn } from '@/lib/utils'

// 7. Types (always use type imports)
import type { User } from '@/types/user.types'
import type { ApiResponse } from '@/types/api.types'

// 8. Styles and assets (if any)
import './styles.css'
```

### Rules

- Always use `import type` for type-only imports
- Use path aliases (`@/`) instead of relative paths when available
- No duplicate imports from the same module — combine them
- Side-effect imports (`import './styles.css'`) go last
- Barrel imports are acceptable for components, avoid for large libraries (tree-shaking)

### Wrong

```tsx
// Don't mix groups or skip blank lines
import { Button } from '@/components/atoms/button'
import { useState } from 'react'
import type { User } from '@/types/user.types'
import { useQuery } from '@tanstack/react-query'
```
