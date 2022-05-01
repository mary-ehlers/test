==First attempt==

```
on:
  push:
  pull_request:
```

Action runs:
1: Pushed branch
2: Created PR
3: Merged PR (pushed to main)

==Second attempt==

```
on:
  push:
    branches-ignore:
      - main
  pull_request:
```

With a purposefully failing CI

Action runs:
1: Pushed branch
2: Created PR (did not prevent merge despite reporting failures)


Added `passing_test` as a "required status check" (had to know the job name to type and select - lame).  This was under Settings -> Branches -> Branch protection rules.

Then the PR refused to merge.

Closed PR.

3: Reopened PR (still failing - no changes made to correct yet)
4: Pushed commit with README file
5: Synchronized PR (still failing?)

Repeated 4/5 for awhile until I got that working.  Moral: push to PR causes two runs of the action.

Merging the PR, however did NOT cause a run.
