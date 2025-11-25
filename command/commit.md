---
description: Stage and commit changes with a well-crafted commit message
agent: repo-manager
subtask: true
---

Analyze the current repository state and create a clean git commit.

$ARGUMENTS

## Instructions

1. Run `git status` to see what's changed
2. Run `git diff` to understand the changes
3. Check recent commit style with `git log --oneline -10`
4. Stage the appropriate files
5. Create a commit with a clear, descriptive message
6. Report the result back

If $ARGUMENTS contains specific instructions about what to commit or the commit message, follow those instructions.

If no arguments provided, analyze all changes and commit them as a logical unit (or suggest splitting if changes are unrelated).
