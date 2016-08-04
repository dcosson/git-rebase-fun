## Git Rebase Fun

Tracking down failure cases when rebasing git branches


## Discoveries

You can see in the history of this project, by either rebasing or merging `feature-a-squashed` into `feature-b`, you get a merge conflict. Feature-b branched directly off of feature-a, so if we hadn't squashed feature a there are trivially no merge conflicts.


A solution to this seems to be, from feature-b, `git rebase feature-a-squashed`



### Example text:

The quick red fox
add a line
