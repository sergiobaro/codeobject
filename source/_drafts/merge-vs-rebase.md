---
title: merge vs rebase
date: 2021-03-08 09:12:55
tags:
---

# Merge vs Rebase


Both of these commands are designed to integrate changes from one branch into another


## Merge
- Pros:
   - Non-destructive

- Cons:
  - Creates a merge commit: poluting the commit history and making it harder to understand

## Rebase
- Pros:
  - Cleaner history: No merge commit and results in a linear history
  - Allows interactive rebasing

- Cons:
  - Creates new commits: 
  - Dangerous if use on public branches

## Thanks to
- [Merging vs. Rebasing | Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)