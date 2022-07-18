---
title: "🔨 Fix missing module error"
date: 2022-07-18
tags: [ "sveltejs" ]
categories: [ "til" ]
---

Within a Svelte project seeing an error such as
`cannot find module '$lib/..' or its corresponding type declarations` can be
resolved by running `npm run prepare`. This will update `tsconfig.json` to add
`$lib` to
[compilerOptions.paths](https://www.typescriptlang.org/tsconfig#paths).
