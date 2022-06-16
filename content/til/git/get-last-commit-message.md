---
title: "📓 Get last Git commit message"
date: 2022-06-16
tags: [ "git" ]
categories: [ "til" ]
---

In a Git repo run `git log -1` to get details of the last commit.

`--pretty` can be used to [format](https://git-scm.com/docs/pretty-formats)
the message according to your needs.

I sometimes just want the subject of the last commit, in which case I run:

```sh
git log -1 --pretty=%s
```
