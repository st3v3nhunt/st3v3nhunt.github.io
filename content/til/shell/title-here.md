---
title: "🐚 Source and export all vars from a file"
date: 2022-06-10
tags: [ "shell" ]
categories: [ "til" ]
---

If you ever need to load a bunch of env vars into an environment it is easily
accomplished by having them listed in a `.env` file e.g.

```sh
# .env
API_KEY=secret
export USERNAME=squirrel
```

If all of the env vars are preceded with `export` the file can simply be
sourced with `source .env`. However, if any of the env vars are not preceded
with `export` there is an option that can be set prior to sourcing the file to
achieve the same result. Running

```sh
set -a; source .env; set +a
```

will load all env vars listed and then turn off the option of exporting all
defined variables.

[Source](https://tldp.org/LDP/abs/html/options.html)
