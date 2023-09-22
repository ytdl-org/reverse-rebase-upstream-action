# Reverse Rebase Upstream Action

This Action is suitable if you:

* are maintaining a fork
* have changes that are not going to be merged into upstream
* want to keep changes based on the latest upstream

The Action rebases your branch on to the upstream branch and commits that as your branch, with new commits from upstream appended. 
If there are conflicts, it simply fails.

In contrast, rebasing the upstream branch onto your branch causes your local changes to be reapplied after new upstream commits.

## Typical usage

```yml
# .github/workflows/sync.yml
name: Rebase Upstream
on:
  schedule:
  - cron: "0 0 * * 0"  # run once a week
  workflow_dispach:    # run manually

jobs:
  sync:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@master
      with:
        fetch-depth: 0  # or greater than the number of commits you made
    - uses: ytdl-org/reverse-rebase-upstream-action@master
      # with:  # all args are optional
      #   upstream: <user>/<repo>
      #   branch:   master
```
