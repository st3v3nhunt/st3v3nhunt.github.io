---
title: ":1234: Do not use include near in count queries"
date: "2014-02-26"
tags: [ "c#", "development", "mongodb" ]
categories: [ "development" ]
highlight: true
---

Using MongoDB to build an API providing some search and filtering
functionality. One of the searches was using the `$near` query. As part of the
call the total number of documents matching the query also needed to be
returned.

There was a query builder responsible for building the queries. Rather than
distinguish between a query for a count and a query to return the documents the
same query was built and used for both operations. During performance testing
there was a noticeable delay in returning data for calls including `$near`
queries.

A bit of investigation and a little more clearer thinking and the `$near` query
element being included within the `count()` query makes no sense whatsoever.
Plus, it is no good for performance. No reduction in the number of results
occurs through `$near` so why would it be included within `count()` queries?
Well, it should not be.

Removing `$near` from `count()` has improved the performance markedly. In this
specific case it reduced the time taken to run the query by at least an order
of magnitude.

A silly oversight that should have been picked up during a code review and one
that could have proved a little more costly than it did, had it not been found
through performance testing. Interesting nevertheless.
