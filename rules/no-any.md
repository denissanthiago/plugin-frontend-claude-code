---
name: no-any
description: Never use the any type in TypeScript
globs: "*.ts,*.tsx"
---

## Never use `any`

The `any` type disables type checking entirely. Always use a specific type instead.

### Use `unknown` when the type is truly unknown
```tsx
// Wrong
function parse(input: any) { return input.data }

// Correct
function parse(input: unknown) {
  if (typeof input === 'object' && input !== null && 'data' in input) {
    return (input as { data: unknown }).data
  }
}
```

### Use generics for flexible functions
```tsx
// Wrong
function getFirst(arr: any[]): any { return arr[0] }

// Correct
function getFirst<T>(arr: T[]): T { return arr[0] }
```

### Use `Record` for dynamic objects
```tsx
// Wrong
const config: any = {}

// Correct
const config: Record<string, string> = {}
```

### Use proper event types in React
```tsx
// Wrong
const handleClick = (e: any) => {}

// Correct
const handleClick = (e: React.MouseEvent<HTMLButtonElement>) => {}
```

### Use type narrowing instead of casting to `any`
```tsx
// Wrong
const value = response as any

// Correct
if (isApiResponse(value)) { /* narrowed type */ }
```

### Exceptions
- `// eslint-disable-next-line @typescript-eslint/no-explicit-any` only when interfacing with a third-party library that has no types and no `@types/*` package available. Always add a comment explaining why.
