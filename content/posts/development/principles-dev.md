---
title: ":three: Development practices and principles"
date: "2021-02-28"
modified: "2021-03-02"
tags: [ "principles", "development", "practices" ]
categories: [ "development" ]
---

During my time working in software development I've picked up a few guiding
principles I try to consistently follow. Some of them have always been the way
I've tried to work and others have been adopted after having been burnt by not
using it in the first place or learning better ways of doing and thinking
about things.

As with almost everything, the context around which I am working impacts on how
closely the principle is able to be implemented but I try to apply them as
often as is appropriately possible.

The principles in this post are closely related to software development
activities and are in no particular order, although I have tried to group
similar ones. It is by no means an exhaustive list of the principles I follow.
I will aim to add to the post every so often as I recall principles and
discover new ones. The definition of the term principle will be stretched here
and there to encompass guidelines and practices too.

This is likely to be the first in a series of posts on ways of working and
thinking I tend to subscribe to.

## Be cautious using `latest`

Whether a Docker image, Helm chart, code dependency or pretty much anything
else you care to think about, using the `latest` version of it needs to be
carefully considered. If the use of `latest` is simply a way of selecting which
version of the thing is going to be used before whatever specific version is
locked down that is fine e.g. during initial and active development of
something. However, using the `latest` in situations where the thing will not
be locked to a specific version and is resolved at build, deploy or runtime is
not a good idea.

Whilst using `latest` might seem like an OK thing to do at face value, and
indeed, there are some situations where it is perfectly OK. Situations such as
initial development and general trialing of something. However, most situations
should require a specific version to be recorded and used. The reason being is
that when using `latest` you are not only putting trust in the creator of the
thing to have correctly working tagging practices but trusting the creator's
ability to maintain access and security controls.

Using `latest`, in some respects makes a bit of a mockery of testing. If you
are testing against the `latest` version of something what have you actually
tested? Is the `latest` version going to be the same tomorrow or next week or
next month?

## **Always** increment `MAJOR` version on any breaking changes

Whenever a breaking a change is made to a public interface the `MAJOR` version
should be incremented. Regardless if the aspects of the interface you
_thought_ should have been private were the only changes. There is a
possibility they were being used and if they were changed without a breaking
change version increment the users of them will not be happy.
The principle of 'if it is available, it will have been used' should be
taken to heart and an expectation that there will be users of it.

## Treat any API the same as you would a web API

By that I mean, if there is an API that is accessible, whether it was meant to
be accessible or not, it should be treated as such. Consequentially, when
breaking changes are made `MAJOR` versions should be incremented to indicate
the change.

## The rule of three

When something has been done for a third time or you know it will be done or
used at least three times it is worth considering doing it in such a way that
it will be reusable. That might entail refactoring some code into a shared
library or module or it might (in relation to the point about automating as
much as possible, below) mean that the activity should be automated.

The rule of three is useful for a couple of reasons. If something has been or
will be used three times it is likely:

* There is something within it that is generic enough that it will be possible
  to extract it into something that is useful to more than three things.
  However, the context needs to be borne in mind to check this will be the
  case
* The details of the reusable bit will be better understood and enable the
  useful bit to be identified and hopefully the majority of the changes that
  would be required in future uses of it

## Use automated release note generation

Something like
[semantic-release](https://github.com/semantic-release/semantic-release) can be
used to automatically create release notes and correctly increment versions.
Ideally an automated release note will satisfy all requirements for all
intended audiences. However, if that isn't the case, having a release note that
is already created will be much easier to add to than one that needs to be
created from scratch.

## Automate as much as possible, whenever possible

Automating as much as possible is a good reason for the purpose of not only
having a system that can perform the task at hand quicker than a human, with
fewer mistakes than a human, it also has the major benefit or codifying the
task.

Codification of the task is a huge benefit as it means it doesn't need to
be maintained in the memory of humans or written down in a non-executable form
(that will become incorrect at some point and ultimately cause confusion as the
humans will not know which is correct). Codifying tasks effectively delegates
the memory storage of the details.

Much like the rule of three (above), the task being automated should be
assessed as to whether it will repay the investment in the automation before
blindly trying to automate it. Some tasks are complex, can be automated easily
and are run many times. However, there are other tasks that are simple, take
significant effort to automate and run infrequently. With the majority falling
between these extremes. There really isn't a golden rule as to when a task
should be automated as it very much depends on the context.

It is worth mentioning that there is the additional benefit of the codification
of the task to take into consideration when deciding whether to automate. If a
task is run infrequently it might very well be the case it is difficult to
recall the steps and it would be beneficial if it could just be run without
having to recall the details, and having those details captured in an
executable form..

## Use a linter

Set a standard for the syntax of the language being used and, as much as
possible (really, it should be a never event), do not change it. Using a linter
to validate and prevent syntax issues being part of code review discussion has
a number of benefits:

* Quicker feedback on issues, no need to wait for a review
* More consistent code as linter will not miss discrepancies like a human would
* No time needs to be spent on
  [bike-shedding](https://en.wikipedia.org/wiki/Law_of_triviality)
* Reviews can focus on important issues

## Health checks

Have some way of accessing key info about what you are building, whether that
is a web frontend or a backend microservice. Something like a health check (as
used by
[Kubernetes](https://kubernetes.io/docs/reference/using-api/health-checks/))
with key information about the thing e.g. the deployed version, memory use, CPU
user, uptime, concurrent users, etc.
