---
name: review
description: Review current code changes by delegating to relevant agents
---

Follow these steps to review the current code changes:

1. Run `git diff` to see all staged and unstaged changes
2. Run `git diff --name-only` to get the list of modified files
3. Analyze the changed files and determine which agents should review them:
   - **TSX/JSX component files** → delegate to `@ux-ui-design` for design and accessibility review
   - **Files with Tailwind classes** → delegate to `@css-optimizer` for class cleanup
   - **Complex components with many hooks/state** → delegate to `@frontend-refactor` for structure review
   - **API integration or form files** → delegate to `@api-integrator` for data flow review
   - **Any file** → delegate to `@performance-auditor` if performance patterns are detected
4. For each relevant agent, send only the changed files for review
5. Compile all agent feedback into a single report organized by:
   - **Critical** — Must fix before committing
   - **Warning** — Should fix soon
   - **Suggestion** — Nice to have improvements
6. If there are Critical issues, list them with the exact file and line number
