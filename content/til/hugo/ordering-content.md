---
title: "↕️  Ordering content"
date: 2022-06-18
tags: [ "hugo" ]
categories: [ "til" ]
---

It is straight forward to order content in Hugo by leveraging front matter
variables. The default order is `Weight -> Date -> LinkTitle -> FilePath`.
It is easy to change the order based on the specific property of interest. See
[lists of content in Hugo](https://gohugo.io/templates/lists/#order-content)
for more information.

The posts in [TIL](/til) are ordered by `weight`. This involved added `weight`
(an integer) to the front matter of the `_index.md` files in the folders within
the `til` folder.

Rather than weight each letter with the place it has in the alphabet the number
has been increased by a factor of 10. This means it will be easy to add another
9 words beginning with the same letter. If it gets to the point of needing more
than 10 words with the same letter the weighting will need to be rejigged,
however, I do not anticipate this being the case.
