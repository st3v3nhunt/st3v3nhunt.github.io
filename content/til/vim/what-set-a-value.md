---
title: "📓 What set this value?"
date: 2024-09-04
tags: [ "neovim" ]
categories: [ "til" ]
---

Ever wanted to know what value a variable has and where it was set from in Vim?

Easy. Just run:

```vim
:verbose set <option>
```

e.g. for textwidth

```vim
:verbose set textwidth
```

The output would look something like:

```sh
textwidth=120
    Last set from ~/code/dotfiles/vim/ftplugin/markdown.vim line 4
```
