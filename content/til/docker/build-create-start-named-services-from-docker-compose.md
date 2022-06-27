---
title: "🪅 Build, create and start named services from Docker Compose"
date: 2022-06-27
tags: [ "docker" ]
categories: [ "til" ]
---

It is possible to
[build](https://docs.docker.com/engine/reference/commandline/compose_build/),
[create](https://docs.docker.com/engine/reference/commandline/compose_create/),
[start](https://docs.docker.com/engine/reference/commandline/compose_start/)
and [up](https://docs.docker.com/engine/reference/commandline/compose_uo/)
a specific service or services from Docker Compose. By default these commands
work with an optional list of services. Each service specified will have the
command run for it.

This is handy should only some of the services want to be started and can come
in handy for testing or just bringing up the DB without all other services.

As an alternative, Compose has the ability to use
[profiles](https://docs.docker.com/compose/profiles/) which can make it easier
to manage selective service actions in larger `docker-compose.yml` files.
