# Merge

Merge a feature branch in the main branch:

```bash
# Checkout the "target" branch
git checkout main

# Merge the feature branch into main
git merge feature-branch

# Disable fast-forwarding (force a merge commit)
git merge feature-branch --no-ff
```