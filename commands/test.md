---
name: test
description: Run tests only for modified files
---

Follow these steps to run tests for modified files only:

1. Run `git diff --name-only` to get the list of modified files (staged and unstaged)
2. Filter only source files (`.ts`, `.tsx`, `.js`, `.jsx`) — exclude config files, markdown, etc.
3. For each modified source file, check if a corresponding test file exists:
   - `ComponentName.tsx` → look for `ComponentName.test.tsx`
   - `use-hook.ts` → look for `use-hook.test.ts`
   - Check both co-located tests and `__tests__/` directories
4. If test files are found, run them:
   ```bash
   npx jest <test-file-1> <test-file-2> --no-coverage
   ```
5. If no test files exist for a modified file, report which files are missing tests
6. Summarize the results:
   - **Passed**: list of passing test files
   - **Failed**: list of failing tests with error details
   - **Missing**: modified files with no corresponding tests
7. If tests fail, analyze the errors and suggest fixes
