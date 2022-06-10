---
title: ":part_alternation_mark: Git aliases"
date: "2016-04-06"
tags: ["aliases", "development", "git"]
categories: ["development"]
---

In order to provide a consistent development environment between team members
as well as making it easier to do physical pair programming sharing a
`.gitconfig` is a good thing to do. After all, when using another person's
machine there are few things more annoying than not having access to the same
shortcuts you rely on.

Git aliases are one of the easier consistencies to bring to a developer's
machine. This is how you can achieve a shared `.gitconfig`.

Add a `.gitconfig` to the repository. This is one I often start with.

```.gitconfig { linenos=true }
[core]
    autocrlf = true
[alias]
    st = status
    hist = log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short
    ci = commit
    com = checkout master
    b = branch
    cob = checkout -b
    co = checkout
[push]
    default = simple
```

Once the `.gitconfig` is in the repo Git needs to be told to use it.

To do that add:

```.gitconfig
[include]
  path = ../.gitconfig
```

To the config file located in the Git directory i.e. `.git/config`.

The manual step not withstanding you now have a `.gitconfig` all members of the
team should be using. It is a good idea to include this information in the
project's `README.md`. And if you were so inclined it could be automated if the
project had some setup scripts to run.
