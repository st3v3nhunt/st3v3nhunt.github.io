---
layout: post
tags: [development, git, branch, fetch]
comments: true
---

After having added a new remote to my local git repository via `git remote add other-remote git@github.com:user/other-repo` I wanted to checkout one of the branches from that remote.

I initially tried `git checkout -b local/branch-name other-remote/feature/branch` and got an error. The problem with trying to do this is there is no information locally about what the newly added remote has. In order to rectify this I ran `git fetch other-remote`. The information about that remote gets downloaded and I am now able to checkout branches from my newly added remote.

References: [git-fetch](https://git-scm.com/docs/git-fetch)
