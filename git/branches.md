# Branches

## Renaming

```bash
# Locally rename the branch
git checkout old-branch
git branch -m new-branch

# Push changes to remote
git push -u origin new-branch

# Delete old remote branch
git push origin --delete old-branch
```

## Deleting

```bash
# Local
git branch -d branch-name

## Remote
git push origin --delete branch-name
```