---
title: "📓 Docker Compose version key is not required after 3.7"
date: 2022-06-20
tags: [ "docker" ]
categories: [ "til" ]
---

From version
[3.8](https://docs.docker.com/compose/compose-file/compose-versioning/#version-38)
of the compose file specification the version key is no longer required.
However, it can be kept for
[information](https://docs.docker.com/compose/compose-file/#version-top-level-element),
if so desired.

In order to run `3.8+` Docker Engine `19.03.0+` is required, see the
[compatibility matrix](https://docs.docker.com/compose/compose-file/compose-versioning/#compatibility-matrix)
for details.

The latest
[Compose file specification](https://docs.docker.com/compose/compose-file/#version-top-level-element)
is a merging of the `2.x` and `3.x` versions and should be the preferred option.
