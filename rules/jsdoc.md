---
name: jsdoc
description: Use JSDoc to document functions, components, interfaces, and type properties in English
globs: "*.ts,*.tsx"
---

## JSDoc Documentation Rules

All documentation must be written in **English**.

### Document all interface and type properties
```tsx
/** User account information */
interface User {
  /** Unique identifier */
  id: string
  /** User's display name */
  name: string
  /** Email address used for authentication */
  email: string
  /** Whether the account is currently active */
  isActive: boolean
  /** Account creation timestamp in ISO 8601 format */
  createdAt: string
}
```

### Document component props
```tsx
interface ButtonProps {
  /** Button style variant */
  variant: 'primary' | 'secondary' | 'outline'
  /** Button size */
  size?: 'sm' | 'md' | 'lg'
  /** Whether the button is in a loading state */
  isLoading?: boolean
  /** Callback fired when the button is clicked */
  onClick?: (e: React.MouseEvent<HTMLButtonElement>) => void
  /** Content to render inside the button */
  children: React.ReactNode
}
```

### Document functions and hooks
```tsx
/**
 * Fetches a paginated list of users filtered by role.
 *
 * @param role - The role to filter users by
 * @param page - Page number starting from 1
 * @returns Paginated user list with total count
 */
function fetchUsers(role: UserRole, page: number): Promise<PaginatedResponse<User>> {}
```

```tsx
/**
 * Manages form submission state with optimistic updates.
 *
 * @param endpoint - API endpoint to submit to
 * @returns Form state and submit handler
 */
function useFormSubmit(endpoint: string) {}
```

### Document React components
```tsx
/**
 * Displays a data table with sorting, filtering, and pagination.
 * Supports server-side and client-side data fetching.
 *
 * @example
 * <DataTable columns={columns} data={users} onSort={handleSort} />
 */
function DataTable<T>({ columns, data, onSort }: DataTableProps<T>) {}
```

### What NOT to document
- Obvious getters/setters (`getName`, `setEmail`)
- Self-explanatory single-line utility functions
- Re-exported types from third-party libraries

### Rules
- Use `/** */` block comments, never `//` for documentation
- One-liner descriptions don't need `@description`
- Use `@param` and `@returns` for functions with non-obvious parameters
- Use `@example` for components with complex usage
- Keep descriptions concise — one sentence when possible
- Every property in an interface or type must have a JSDoc comment
