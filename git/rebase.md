# Rebase

When rebasing, it is the opposite method to merging. When rebasing, is it the branch that you are making a change to so you need to checkout the branch and then rebase onto that.

```bash
git checkout feature-branch  
git rebase main
``` 

## Benefits

1. The person doing the rebase will resolve the conflict before the pull request.
2. Clarity - you might want to rebase so that when you merge, it’ll fast-forward merge.
3. Using interactive rebasing, you can squash commits that don’t really require their own commits.  

You can always bail on a rebase at any time by using:

```bash
git rebase --abort
``` 

If you hit conflicts along the way you will need to resolve them, add the files and then do:

```bash
git rebase --continue
```  

This is what it looks like when you are in the middle of a rebase:

```
rebase in progress; onto c9abe1b  
You are currently rebasing branch 'feature' on 'c9abe1b'.  
  (fix conflicts and then run "git rebase --continue")  
  (use "git rebase --skip" to skip this patch)  
  (use "git rebase --abort" to check out the original branch)  
  
Unmerged paths:  
  (use "git restore --staged <file>..." to unstage)  
  (use "git add <file>..." to mark resolution)  
        both modified:   config.txt  
  
no changes added to commit (use "git add" and/or "git commit -a")
```

Once you have added the file that was conflicted, you will progress to this status:

```
rebase in progress; onto c9abe1b  
You are currently rebasing branch 'feature' on 'c9abe1b'.  
  (all conflicts fixed: run "git rebase --continue")  
  
Changes to be committed:  
  (use "git restore --staged <file>..." to unstage)  
        modified:   config.txt
```

At this point, you can `git rebase --continue` and you should be able to proceed to the next patch.

## Interactive rebase

This will rebase the last 2 commits:

```bash
# f61d5e0 (HEAD -> new-branch) Combination of loads of commits  
# 3f4f4a1 Commit for feature 5  
# 74bf605 (master) Commit for feature 4  
  
git rebase -i HEAD~2
```

You can also use `git rebase -i 74bf605` but this is slightly less intuitive because you have to use the commit hash of the previous commit. The `HEAD~2` syntax is clearer to me.

> [!warning]
> Interactive rebase appears in ***chronological*** order, so it is the reverse order to what you see in `git log`.

```
reword 3f4f4a1 New feature completely built
squash f61d5e0 Combination of loads of commits
```

> [!warning]
> After an interactive rebase, your **commit hashes will change**. When you come to push your changes, you will need to force push.
