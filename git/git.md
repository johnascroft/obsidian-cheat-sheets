# Git

## Common commands

- [[merge]]
- [[rebase]]
- [[remote]]

## Move commits to another branch

Say if you’ve committed on the `main` branch and meant for it to be on another side branch, you can do the following. It will branch off from where you left off (but not checkout the branch), then you roll-back master, then move to the new branch.

```bash
git branch new-branch  
git reset --hard HEAD~3 # You can also use the commit hash in place of HEAD~3  
git checkout new-branch
```

## Delete local branch

```bash
git branch -d branch-name
```

## Delete remote branches

```bash
git push origin --delete branch-name
```