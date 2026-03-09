---
name: commit
description: Commit only the files that were changed in the current session
---

Follow these steps to commit only the changed files:

1. Run `git status` to see all modified and untracked files
2. Run `git diff` to review the actual changes (staged and unstaged)
3. Run `git log --oneline -5` to check the recent commit style
4. Analyze the changes and draft a concise commit message that:
   - Summarizes what was done (not how)
   - Follows conventional commits format: `feat:`, `fix:`, `refactor:`, `style:`, `docs:`, `test:`, `chore:`
   - Is written in English
5. Stage ONLY the files that were modified — use `git add <file1> <file2> ...` with explicit paths. Do NOT use `git add .` or `git add -A`
6. Do NOT stage files that contain secrets (.env, credentials, tokens)
7. Create the commit using a HEREDOC:

```bash
git commit -m "$(cat <<'EOF'
<type>: <short description>

Co-Authored-By: Claude Opus 4.6 <noreply@anthropic.com>
EOF
)"
```

8. Run `git status` to verify the commit was successful
