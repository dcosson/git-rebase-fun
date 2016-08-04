## Git Rebase Fun

Tracking down failure cases when rebasing git branches


## Discoveries

You can see in the git history of this project that by either rebasing or merging `feature-a-squashed` into `feature-b`, you get a merge conflict. Yet `feature-b` branched directly off of `feature-a`, so if we hadn't squashed there couldn't be merge conflicts.


A solution to this seems to be, from feature-b, run `git rebase -Xtheirs feature-a-squashed`.

The real-world scenario we were simulating though is when `feature-a-squashed` gets rebased onto master, and master might have some other commits in the meantime that `feature-b` doesn't have. But the following commands (run from `feature-b`) should work in that case:

```
git fetch
git merge origin/master^
git rebase -Xtheirs origin/master
```

There's a quirk that now all the individual commits in feature-a still exist in feature-b, but those can be squashed later. For instance you could run `git rebase -i $(git merge-base HEAD origin/master)^` and then manually `fixup` the commits you no longer want.


### Example text:

The quick red fox
add a line
