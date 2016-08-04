## Git Rebase Fun

Tracking down failure cases when rebasing git branches


## Discoveries

You can see in the git history of this project that by either rebasing or merging `feature-a-squashed` into `feature-b`, you get a merge conflict. Yet `feature-b` branched directly off of `feature-a`, so if we hadn't squashed there couldn't be merge conflicts.


However, there seems to be a simple solution. You should rebase, and since you know that all the conflicting commits from `feature-a` are exactly the same as the merge commit, whenever the merge conflicts come up you should be able to just run `git rebase --skip` like it suggests and it'll work out.


If you were running this where `feature-a-squashed` was actually the tip of master (say feature-a was PR that went out and you rebase PR's to the tip of master instead of merging to keep a linear history), you'd probably also want to run `git merge origin/master^` before `git rebase origin/master`, to separately resolve any other conflicts you might have with master before the rebase where you'll skip all conflicts.


### Example text:

The quick red fox
add a line
