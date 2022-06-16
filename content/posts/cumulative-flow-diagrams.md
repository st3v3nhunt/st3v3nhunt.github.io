---
title: "📈 Cumulative flow diagrams"
date: "2013-09-13"
tags: [ "agile" ]
categories: [ "development" ]
---

## What is a CFD?

A CFD is a graph showing the state of the work over a period of time based on
data acquired from
[Kanban](http://st3v3nhunt.tumblr.com/post/61110223853/what-work-has-work-where-working-work-wrangles-waiting).

More in-depth explanations available at
[Wikipedia](http://en.wikipedia.org/wiki/Cumulative_flow_diagram),
[Google](https://www.google.co.uk/?#q=kanban) and
[David J Anderson](http://edn.embarcadero.com/article/32410).

## Graphs and colours…I want one

To create a CFD is pretty straight forward. The number of stories in each state
represented on the board need to be recorded on a regular basis. Daily is
typical. With the data a chart can be generated, plotting the accumulated data
against time.

## Colours are great but why do I *need* one?

There is a host of reasons why using CFDs are a good idea. Personally, I like
the fact that from a relatively small amount of easily obtainable data a huge
amount of information can be discovered. The information can provide some very
revealing insights into the flow of the work.

## Insights sound interesting, like what…

It is probably best to use a real world example. The commentary and insights
below were gained after studying this CFD.

![Cumulative Flow Diagram](/images/cfd.png)

The CFD is from a project where the time and cost were fixed with the scope
being variable. Effectively a time box where as much as possible was to be
delivered.

### Backlog (ideas hangout)

* Although there are stories added throughout the duration of the project there
  are a couple of big bangs (19/08 & 31/08). Ideally all stories should be
  added on a regular, free flowing basis.
* Approximately 40% of the stories created were not done - how much time was
  spent on creating the stories that were effectively wasted (not much)?

### Refinement (ideas thought about)

* There were always some stories being 'refined'. One might assume that is a
  good thing as stories were always being thought about and made ready for
  development.

### UX & Design (interface)

* The state was only used within the first couple of weeks. This might have
  been due to that being the time when the front end was being designed and
  refined before it was developed.

### Ready to go (blast off)

* A large number of stories were ready to go in week 2, for the full week. Not
  one story moved from this state during the week. Not a good thing, the board
  will have looked pretty stagnant at this time.
* A couple of stories ended the time box as being refined - this means time and
  effort was spent on doing the work to get them into this state and that was
  wasted.

### In progress (rolling)

* Week 3 saw many stories in progress, perhaps too many. How many people were
  in the team and how many of the stories were actually being worked on? Were
  there blockers stopping the progress of the stories?

### Ready to verify (awaiting testing)

* Stories were not sat in the queue for very long. Actively being tested as
  soon as available.
* Bit of queue building up towards the end of the time box, was this caused by
  the knowledge the time was closing?

### Verfying (is it ok)

* Some stories were stuck in verifying for a long time. Possibly there was no
  environment available to complete the verification?

### Verified (done the thing right)

* Some of the stories are in verified for a small period of time, suggesting
  they were accepted almost immediately.
* The last week or so saw a few stories stack up in verified. This was due to
  environment problems. Once that was sorted the stories quickly moved into
  accepted.

### Accepted (done the right thing)

* It was 2 weeks before anymore than 2 stories were accepted.
* It looks like the stories were accepted in chunks rather than when they were
  *ready* to be accepted. Is this due to the person accepting them not being
  available or engaged or some other reason?

### Waste (…)

* The stories added around 19/08 - were they wasted 27/08? If so, why were they
  created and perhaps this should not happen in the future?
