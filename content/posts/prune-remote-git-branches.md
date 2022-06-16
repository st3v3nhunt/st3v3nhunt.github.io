---
title: "✂️  Prune remote git branches"
date: "2015-07-23"
tags: [ "branch", "git", "prune" ]
categories: [ "development" ]
---

Using `git branch -r` to check the list of branches on the remote can often
lead to a long list of branches making it difficult to tell which are active
e.g.

![All branches](/images/stale-branches.png)

The list is easily trimmed to only those that are active. Git calls this
pruning and is achieved via `git remote prune origin`.
There is a test mode activated by the flag `--dry-run` e.g. `git remote prune
origin --dry-run`, resulting in output like this:

![Branches to prune](/images/branches-to-prune.png)

When run without the flag (`git remote prune origin`) the branches are pruned
as so:

![Pruned branches prune](/images/pruned-branches.png)
