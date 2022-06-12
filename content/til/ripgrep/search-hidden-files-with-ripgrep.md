---
title: "🔍 Search hidden files with ripgrep"
date: 2022-06-12
tags: [ "ripgrep" ]
categories: [ "til" ]
---

[ripgrep](https://github.com/BurntSushi/ripgrep) is an excellent alternative to
[grep](https://en.wikipedia.org/wiki/Grep). One of its benefits is how it
[filters](https://github.com/BurntSushi/ripgrep/blob/master/GUIDE.md#automatic-filtering)
the files it searches.

However, on occasion those normally ignored files need to be searched. I find
this is especially the case when searching through my
[dotfiles repo](https://github.com/st3v3nhunt/dotfiles). Adding the flag
`--hidden` or `-.` does the job e.g.

```sh
rg -. <search_term>
```
