# [st3v3nhunt.github.io](https://st3v3nhunt.github.io/) blog source

> This repo contains the source for
  [st3v3nhunt.github.io](https://st3v3nhunt.github.io)

The blog uses the [hyde-hyde](https://themes.gohugo.io/hyde-hyde/) theme and is
generated by [Hugo](https://gohugo.io/).

It is hosted on [GitHub Pages](https://pages.github.com/).

## Clone repo

Clone the repo and submodules:

```sh
git clone https://github.com/st3v3nhunt/st3v3nhunt.github.io
git submodule update --init --recursive
```

## Workflow

1. Create new posts manually or via Hugo's CLI e.g.
[`hugo new`](https://gohugo.io/commands/hugo_new/).

1. Run the site locally (to check the content) via `hugo server`.

1. When happy with the new content, push the changes to the remote. GitHub
   Actions will generate the content into `./public` on the `gh-pages` branch.
