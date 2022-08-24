---
title: "📓 Access env vars in Neovim"
date: 2022-08-24
tags: [ "neovim" ]
categories: [ "til" ]
---

Accessing an environment variable within Neovim from a lua script is straight
forward. It is just a case of calling `vim.env.env-var-name` where
`env-var-name` is the name of the environment variable e.g.

```lua
local homebrew_prefix = vim.env.HOMEBREW_PREFIX
print(homebrew_prefix)
```

Would print the value of the `$HOMEBREW_PREFIX` env var.
