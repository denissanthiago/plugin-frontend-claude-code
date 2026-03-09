# Plugin Frontend

Claude Code plugin for frontend development: React, Next.js, TypeScript, Tailwind, react-query, React Hook Form, Redux Toolkit, Yup, React Testing Library, Jest.

## Installation

```bash
claude --plugin-dir /path/to/plugin-frontend
```

Or create a symlink in your project for persistent use:

```bash
mkdir -p .claude/plugins
ln -s /path/to/plugin-frontend .claude/plugins/plugin-frontend
```

## Recommended Configuration

After installing this plugin, add the following configuration to your user-level settings file:

**File:** `~/.claude/settings.json`

```json
{
  "skipDangerousModePermissionPrompt": true,
  "env": {
    "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1",
    "teammateMode": "auto"
  }
}
```

### What each option does

| Key | Description |
|---|---|
| `skipDangerousModePermissionPrompt` | Skips the dangerous mode confirmation prompt for smoother execution |
| `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS` | Enables experimental agent teams functionality |
| `teammateMode` | Sets teammate mode to `auto` for automatic agent collaboration |

## Included MCPs

### Chrome DevTools

Activated automatically. Provides:

- Browser screenshots and snapshots
- Console and network inspection
- Click, form, and navigation automation
- Lighthouse audits (accessibility, SEO, performance)
- Performance traces and memory snapshots
- Mobile device emulation

**Requirements:** Node.js v20.19+ and Chrome stable (136+)

**Connect to Chrome with authenticated session (optional):**

```bash
google-chrome --remote-debugging-port=9222 --user-data-dir="$HOME/.chrome-debug-profile"
```

Then update the plugin's `.mcp.json` to add `--browserUrl=http://127.0.0.1:9222` to the args.

### Figma

Activated automatically via the official Figma remote MCP server. Provides:

- `get_design_context` — Extracts component structure, layout rules, and styles from a Figma selection
- `get_variable_defs` — Extracts design tokens (colors, spacing, typography)
- `get_code_connect_suggestions` — Maps Figma nodes to existing code components
- `generate_diagram` — Generates FigJam diagrams from Mermaid syntax

On first use, Claude will prompt you to authenticate with your Figma account.

## Agents

| Agent | MCPs | Description |
|---|---|---|
| `ux-ui-design` | Figma, Chrome DevTools | Design review, responsive audit, and accessibility checks |
| `component-builder` | Figma | Creates React components with atomic design, TypeScript, and Tailwind |
| `performance-auditor` | Chrome DevTools | Core Web Vitals, bundle size, lazy loading, and caching optimization |
| `css-optimizer` | Figma | Tailwind cleanup, redundancy removal, dark mode, and v4 migration |
| `frontend-refactor` | — | Extract hooks, improve composition, reduce re-renders |
| `api-integrator` | — | API integration with React Query, React Hook Form, and Yup validation |
| `test-writer` | — | Generates tests with React Testing Library and Jest |

### How to use agents

Agents are available as teammates that Claude can delegate to automatically, or you can invoke them directly.

**Direct invocation from the chat:**

```
@ux-ui-design review the LoginPage component for accessibility and responsive issues
```

```
@component-builder create a Button atom from this Figma: <figma-url>
```

```
@performance-auditor audit the dashboard page for Core Web Vitals issues
```

```
@css-optimizer clean up Tailwind classes in src/components/ and compare tokens with Figma
```

```
@frontend-refactor refactor UserProfile.tsx - extract logic into custom hooks
```

```
@api-integrator connect the /api/users endpoint with react-query and create a form with Yup validation
```

```
@test-writer write tests for the Button and UserCard components
```

**Automatic delegation:** With `teammateMode: "auto"` enabled in your settings, Claude will automatically delegate tasks to the appropriate agent based on context. For example, if you ask Claude to "create a Card component", it will route the task to `component-builder`.

**Tips:**
- Pass a Figma URL to `component-builder` to build components that match the design exactly
- Chain agents: ask `ux-ui-design` to review what `component-builder` created
- Use `css-optimizer` with a Figma URL to ensure code tokens match the design system
- Use `performance-auditor` after building features — it runs Lighthouse and performance traces automatically
- Use `api-integrator` when connecting new endpoints — it handles the full flow (types, hooks, forms, validation)
- Use `test-writer` after creating components to ensure test coverage

## Rules

| Rule | Applies to | Description |
|---|---|---|
| `tailwind-clsx` | `*.tsx, *.jsx, *.ts, *.js` | Always use Tailwind for styling and clsx for conditional classes |
| `no-any` | `*.ts, *.tsx` | Never use the `any` type in TypeScript |
| `jsdoc` | `*.ts, *.tsx` | Document functions, components, interfaces, and properties with JSDoc in English |
| `naming-conventions` | `*.ts, *.tsx, *.js, *.jsx` | PascalCase components, camelCase hooks/functions, kebab-case files |
| `import-order` | `*.ts, *.tsx, *.js, *.jsx` | Consistent import order: react > next > libs > components > hooks > utils > types |
| `no-console` | `*.ts, *.tsx, *.js, *.jsx` | No `console.log` in production code, only `console.error` allowed |

## Commands

| Command | Description |
|---|---|
| `commit` | Commits only the files that were changed, using conventional commits format |
| `review` | Reviews current code changes by delegating to relevant agents |
| `test` | Runs tests only for modified files and reports missing coverage |

## Hooks

| Event | Trigger | Action |
|---|---|---|
| PostToolUse | Edit or Write on `.ts, .tsx, .js, .jsx, .css` | Runs Prettier and ESLint on the modified file |
| Stop | Agent finishes | Runs `tsc --noEmit` to verify no TypeScript errors |

## LSP Integration

TypeScript Language Server is configured via `.lsp.json` to provide real-time diagnostics for `.ts`, `.tsx`, `.js`, and `.jsx` files.

## Included Skills

- `atomic-design-fundamentals` — Component architecture
- `clean-code` — Clean code principles
- `design-patterns-implementation` — Design patterns
- `next-best-practices` — Next.js 15+
- `react-hook-form` — Optimized forms
- `react-query` / `react-query-best-practices` — Async state management
- `tailwind-design-system` — Tailwind v4
- `typescript-advanced-types` — Advanced types
- `vercel-react-best-practices` — Vercel React patterns
- `web-design-guidelines` — Web design guidelines
