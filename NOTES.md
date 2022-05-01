# Legend

| Symbol | Meaning |
| ---- | --- |
| :heavy_check_mark: | Github Action triggered and succeeded |
| :x: | Github Action triggered and failed |
| :leftwards_arrow_with_hook: | Merge allowed |
| :heavy_exclamation_mark: | Merge not allowed |

# First attempt

```
on:
  push:
  pull_request:
```

| Event | Effects |
| --- | --- |
| Pushed branch | :heavy_check_mark: |
| Created PR | :heavy_check_mark: :leftwards_arrow_with_hook: |
| Merged PR | :heavy_check_mark: |

# Second attempt

```
on:
  push:
    branches-ignore:
      - main
  pull_request:
```

| Event | Effects |
| --- | --- |
| Pushed branch with a purposefully failing CI | :x: |
| Created PR | :x: :leftwards_arrow_with_hook: |
| Added branch protection rules | :heavy_exclamation_mark: |
| Closed PR |  |
| Reopened PR (no changes) | :x: :heavy_exclamation_mark: |
| Pushed commit (not fixed) | push: :x: synchronize: :x: :heavy_exclamation_mark: |
| Pushed commit (fixed) | push: :heavy_check_mark: synchronize: :heavy_check_mark: :leftwards_arrow_with_hook: |
| Merged PR |  |

NOTE: Settings -> Branches -> Branch Protection Rules: had to know the job name (the key value under `job:` in the yaml) to start typing in the box in order for something to show up that was selectable.

# Third attempt

```
on:
  push:
```

| Event | Effects |
| --- | --- |
| Pushed branch | :heavy_check_mark: |
| Created PR | :leftwards_arrow_with_hook: |
| Pushed commit to add purposefully failing test | :x: :heavy_exclamation_mark: |
| Rebased to remove last commit; force pushed | :heavy_check_mark: :leftwards_arrow_with_hook: |
| Merged PR | :heavy_check_mark: |

# Fourth attempt

```
on:
  pull_request:
```

| Event | Effects |
| --- | --- |
| Pushed branch |  |
| Created PR | :heavy_check_mark: :leftwards_arrow_with_hook: |
| Pushed additional commit | :heavy_check_mark: :leftwards_arrow_with_hook: |
| Merged PR |  |
