---
title: "🖥️  App specific domain names for local dev"
date: 2021-09-24
tags: [ "development", "practices", "microservices" ]
categories: [ "development" ]
---

A common architectural style (at the time of writing) is to split up
applications into many, smaller, more focussed applications. Frequently this
style is known by the term `microservices`. When working with microservices
I've rarely had the need to run, and actually use, more than a single web
application concurrently in my development environment.
> I'm using the term `web application` here to mean a web site as opposed to an
> API with an HTTP
> interface. A major difference being that a web site will use cookies for
> authentication, saving session data, preventing
> [Cross Site Request Forgery](https://owasp.org/www-community/attacks/csrf),
> etc. And, although a web based API will likely need some of the same features
> these are often handled by a separate layer such as an API Gateway.

For systems with several web apps wishing to be run locally, at the same time,
an issue can occur with cookies clashing. Cookies are specific to domains and
paths. The key name against which values are stored can be
different, however, for sites using libraries to handle cookie configuration it
is common for the key to be the same. Therefore, it is likely different web
apps running on the same host will end up
reading and writing the same values. This causes issues with unexpected values
being present, often resulting in the web app breaking.

Running the apps on different ports e.g.
[http://localhost:5000](http://localhost:5000),
[http://localhost:8080](http://localhost:8080), doesn't help as cookies have no
notion of port.

There are several ways to work around this. Perhaps the easiest option, for
situations with two sites is to access one site using `localhost` and the other
site with `127.0.0.1`. Doing so provides each web app with its' own cookie and
fixes the cookie clashing issue.

However, for situations with more than two web apps a different approach is
required. A good option is to create domain names on the development machine,
one for each web app. To do so, entries can be added into the machine's
[hosts file](https://en.wikipedia.org/wiki/Hosts_(file)) e.g.

```sh
127.0.0.1 admin-web.localhost
127.0.0.1 super-user-web.localhost
127.0.0.1 user-web.localhost
```

This results in being able to access as many different web sites as is
required. Additional benefits to using this approach include:

* Password managers will store each domain separately, preventing many, many
  entries accumulating for `localhost`. An added bonus is deciding which password
  to use is much easier if there is only a single choice!
* The name of the subdomain can be meaningful, potentially mapped to the name
  of the code repo, helping understand which code is running which site.
* Ports become unnecessary for differentiating between web apps.
* Other web based applications that run locally can have bespoke subdomains
  created for them e.g.
  [RedisInsight](https://redis.com/redis-enterprise/redis-insight/) and
  [pgAdmin](https://www.pgadmin.org/).

It is worth noting the domain name does not need to be a subdomain of
`localhost`, however, doing this is useful as `localhost` is a
[reserved](https://en.wikipedia.org/wiki/.localhost) domain name and is treated
in a special by many applications. This includes web browsers which will alert
you of accessing sites that are not secure unless they are served from the
`localhost` [TLD](https://en.wikipedia.org/wiki/Top-level_domain).
