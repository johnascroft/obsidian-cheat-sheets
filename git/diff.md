# Diff

Shows the diff of things I haven't staged for commit yet:
```bash
git diff
```

Show the diff of things I am about to commit:
```bash
git diff --staged
```

Shows the diff of things between where I am now and `HEAD` (which is the thing that is about to become the parent of my next commit):

```bash
git diff HEAD
```