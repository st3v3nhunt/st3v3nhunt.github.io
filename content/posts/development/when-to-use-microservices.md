---
title: ":microscope: When to Use Microservices (And When Not to!)"
date: 2020-09-14
tags: [ "development", "microservices" ]
categories: [ "development" ]
---

I watched
[When To Use Microservices (And When Not to!)](https://www.youtube.com/watch?v=GBTdnfD6s5Q)
soon after it was published but never got round to publishing this post, which
I wrote at the same time but have edited more recently so I could publish it.
The post contains some thoughts I had about the video and thought it would be
worth capturing them and maybe try to get back into blogging at some regular
interval, although clearly that didn't happen at the time...

## TL;DR

The video is relatively short and worth the time to watch. It is an overview
and comparison or microservices and monoliths. Sam does a good job of
highlighting the difficulties and challenges around 'doing' microservices,
provoking thought on the subject.

I've not seen a GOTO video in this style before (and as it turns out five
months later I've not seen another like it either). I _think_ I like it. It
certainly makes the video easier to digest in chunks and provides a breakdown
of the key takeaway points which can be useful when reviewing the video
yourself or discussing with others.

## My Commentary

In order to provide some structure, I'll cover the different themes from the
video.

### Change is Hard

I totally agree with the sentiment of how the people side of change is really
hard and actually making things change, in a lasting way, is incredibly tough.
Without having any empirical data I would imagine change is likely doomed to
fail most of the time. Perhaps in a similar vein to how a gambler only ever
tells you about their success people only ever tell you about successful
changes...

From my experiences, I think changing the ways of working within an
organisation needs to originate from where the power-base resides. By
power-base I mean the group of people (sometimes an individual) that can veto
decisions and has the final say on whether something is going to happen or not.
In some organisations that will be product development team(s) and they will be
able to tread a path that will be followed by others. However, I think for a
lot of organisations the power resides in the operational teams. If change is
attempted without the operational team either leading it, or at the very least
being heavily involved, the change is likely going to fail. I've seen product
development teams attempt to make changes with the hope that others will follow,
however, as it is ultimately the operations teams that are responsible for the
running of the product, the change hits a hard stop at the boundary of the
product development team's sphere of influence.

Of course there are other power-bases within organisations but it often ends up
being held by a small number of people or perhaps a individual. Some
organisations operate by diktat and when one arrives from on high, that can
force change. However, the forcing of change is generally not an effective way
to achieve change. It may achieve rapid change in the short term but there are
likely longer term issues having the ground work laid to causes problems in the
future. Forced change also risks getting exactly what was asked for as opposed
to being the change that the sentiment intended, thus loosing the benefits of
making the change in the first instance.

In my experience, achieving change is much easier when the change is being
instigated by the people that build the thing and run the thing. The reason
this works is that the sphere of influence of that team encompasses everything
where change will happen.

Just how many organisations have this setup?
I wish it were more but there are many reasons why it isn't common. One of them
being the idea of dev-ops is much newer than the how long organisations have
been around and changing an organisation from one where development and
operations are separate to one where they are working together, even moderately
so is yet more change and as we know now, change is difficult. Sam touched on
it briefly towards the end of the video, asking a team of people who have never
been on call to start doing it isn't as easy as it sounds. Often the financial
reward isn't commensurate with the sacrifices (either perceived or real)
required. In this case it can boil down to whether the person really cares
about the thing they are working on, in some cases that isn't going to be a
problem but in others it most certainly will be. And of course going on call
may well require contracts to be renegotiated which be tricky.

I've thought about this issue on and off in the time between drafting and
publishing this post. I'm at the stage of believing a lot of the problems
around change are due to the culture of an organisation along with the
structure.
If an organisation's culture is one built on minimising change then it is going
to be much more difficult to make meaningful and lasting change.
If the culture is one of adaptability and embracing change then making internal
changes is likely going to be easy.
I'll get round to writing more about organisation culture at some point.

### Using Microservices

Touching on the reasons for using microservices, it was interesting how Martin
picked up on highlighting the business benefits of having independent
deploy-ability such as lowering risks and providing business units/product
teams with more autonomy (linking into the communication interfaces of APIs)
rather than focussing on having this often nebulous ability to deploy things
independently. Deploying with zero down time is interesting as although it has
a business benefit (and an easy non-functional requirement to say is a must),
it depends on the business as to how much value it really is.

Thinking about how this applies to my experiences, I've seen really robust,
slick deployment capabilities be somewhat wasted as the 'continuous delivery'
pipeline stopped before deploying to the production environment. And the
production environment deployment was handled in a totally different manner.

If the continuous delivery pipeline doesn't end in delivering the product to
the production environment I'm no sure how accurate it is to call it continuous
deliver. Maybe if it is contextualised e.g. 'a continuous delivery pipeline to
staging' (or whatever is the last environment) at least this makes it clear it
isn't a complete delivery pipeline.

This brings me onto deployments and how things are actually done.

### Deployments

A major benefit to microservices over monoliths is their independent
deploy-ability. However, I'd argue this doesn't matter if the deployments
aren't done frequently (resulting in many changes being bundled together across
many microservices) or they are done in such a way that all microservices
within the larger system are deployed in one go. This might have been what was
referred to in the video when Sam mentioned an organisation that had been able
to deploy independently at some point but never did it and as a result lost the
capability.

Why bother with the cost of the flexibility of being able to do something if
the reality is that it is never utilised. It is analogous to buying a vehicle
with seven seats and loads of luggage space and only ever using it to drive
yourself around. It might be really flexible but the reality is not only did it
cost more to purchase in the first place there is an ongoing cost of
maintaining the larger vehicle.

This leads onto the mention of the cost of things.

### Costs of Doing Things

It was good to hear a bit of discussion about thinking about the costs of doing
things. It seems really common for solutions to be chosen because they could
solve everything and could be extended to cater for all eventualities but the
reality is that there is a cost involved in having that level of flexibility
and most of the time this isn't thought about too much.

What is the cost of having a system be so generic and abstract when trying to
develop things or maintain those things or run those things?
Where does the domain knowledge reside?
Does it get spread throughout multiple systems with different teams
being responsible for the different systems?

I've seen a system just like this go from a configurable master-piece where no
development resource was ever going to be required to something that needed
development input regularly as edge cases were discovered and the complexity of
the system became overbearing.
The result being a very costly system in every aspect of its life cycle, from
design to development to maintenance. To the ability to understand the
implications of changes to it and by it.
Not the way to go.

### Communication via APIs/Microservices

Linked to the challenge of making changes is difficulties in communication
across large groups, mainly because people are people. I'm very much a
proponent of providing interfaces between teams in the form of APIs and
microservices as it leaves no room for interpretation, at least that is the
idea, obviously it doesn't always work in practice.

## Summary

This post is quite long and wordy, fortunately I've added a TL;DR which can be
reduced further to just recommending the video is watched. Along with stating
that context is everything when deciding whether to use microservices or not.
