---
name: naming-conventions
description: Enforce consistent naming conventions across the codebase
globs: "*.ts,*.tsx,*.js,*.jsx"
---

## Naming Conventions

### Files and directories
- **kebab-case** for all file and directory names
- Components: `button-group.tsx`, `user-profile.tsx`
- Hooks: `use-auth.ts`, `use-form-submit.ts`
- Utils: `format-date.ts`, `parse-query.ts`
- Types: `user.types.ts`, `api.types.ts`
- Tests: `button-group.test.tsx`

### Components
- **PascalCase** for component names and their types

```tsx
// File: button-group.tsx
function ButtonGroup({ children }: ButtonGroupProps) {}
```

### Hooks
- **camelCase** prefixed with `use`

```tsx
// File: use-auth.ts
function useAuth() {}
function useFormSubmit() {}
```

### Functions and variables
- **camelCase** for functions, variables, and parameters

```tsx
const userName = 'John'
function formatDate(dateString: string) {}
const handleClick = () => {}
```

### Constants
- **UPPER_SNAKE_CASE** for true constants and env variables

```tsx
const MAX_RETRIES = 3
const API_BASE_URL = process.env.NEXT_PUBLIC_API_URL
```

### Types and interfaces
- **PascalCase** for types and interfaces
- Suffix props with `Props`, context with `Context`, state with `State`

```tsx
interface UserCardProps {}
interface AuthContext {}
type FormState = 'idle' | 'loading' | 'error'
```

### Enums
- **PascalCase** for enum name, **PascalCase** for members

```tsx
enum UserRole {
  Admin,
  Editor,
  Viewer,
}
```

### Event handlers
- Prefix with `handle` in implementation, `on` in props

```tsx
interface ButtonProps {
  onClick: () => void    // prop: on + Event
}

function Parent() {
  const handleClick = () => {}  // handler: handle + Event
  return <Button onClick={handleClick} />
}
```
