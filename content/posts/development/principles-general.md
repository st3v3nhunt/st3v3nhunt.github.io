---
title: ":golf: General working principles"
date: "2021-03-04"
tags: [ "principles", "development", "practices" ]
categories: [ "development" ]
---

Following on from the post about
[development practices and principles](../principles-dev/)
I wanted to capture principles more related to general ways of thinking and
working. As before, this isn't in any particular order.

## Break work down into as small chunks as it practicable

If there is a large piece of work to be done, breaking it down into smaller
chunks is generally a good idea. The chunks should be as small as makes sense
within the context of where and how the work is happening. This is pretty much
the idea behind the adage of trying to
[eat an elephant](https://en.wiktionary.org/wiki/eat_an_elephant_one_bite_at_a_time)
[one bite at a time](https://www.psychologytoday.com/gb/blog/mindfully-present-fully-alive/201804/the-only-way-eat-elephant).

There are both benefits and considerations (not necessarily cons) for chunking
up work. The benefits of smaller chunks of work include:

* Taken on their own, they are less complex
* It is easier to understand the dependencies between the chunks and work out
  which can be done in parallel, ideally leading to the ability (if there is
  the capacity) for the overall piece of work to be completed more quickly
* Having a unit of measurement i.e. a chunk of work from which a forecast can
  be generated (once there are some complete chunks) for remaining effort
* Identifying points to reflect on and assess what has been achieved, the value
  gained, whether it is worthwhile continuing, etc. are possible whereas if the
  work is a single thing that isn't possible until the end

Considerations for chunking up the work include:

* Breaking work into chunks is more art than science and as such it isn't going
  to be 'correct' (as there are several ways of doing it and it is likely going
  to vary by when it is done, by whom, what they know at the time, etc.)
* Overall, the complexity of the work is likely to remain, it is just going to
  be moved around and its nature might change. The individual pieces of work
  should be simpler but there are likely going to be dependencies between them
  that will need to be managed and understood

## Consider what isn't there as much as what is

I think of this as a good practice mainly when reviewing code changes but it is
much more applicable than that.

When I'm doing code reviews, along with reviewing the things that _have_
changed, I try to think about what _hasn't_ changed.

Is there something that should have been changed? Perhaps some documentation
needs to be updated or maybe another system is relying on some part of the
application's interface that isn't immediately obvious as an external interface.
The format of a generated file picked up by another system perhaps? Of course,
in an ideal world this type of change would have a thorough and robust set of
tests to ensure changes to it were flagged up. However, that isn't always going
to be the case and there is some stuff that just won't be possible to test (at
least with a reasonable cost).
Understanding or at least having knowledge of the implications for changing
systems beyond the system itself can be very valuable.

An indicator of not thinking like this can be an immediate approval of a code
review. Whilst a very quick review is sometimes appropriate and can be welcome
(after all, it means the code was good, doesn't it?!). I do worry it
hasn't been given the appropriate level of scrutiny it deserves.

When reviewing code I always feel a little disappointed in myself if I can't
find at least one thing to comment on.

## Maximise work not done

I'm not sure everybody would agree with this sentiment but I think it is
important to maximise the work not done. By which I mean I only want to be
doing work that is valuable, whether that is for myself or for my employer. It
is a good job my definition of valuable is quite broad! Ideally the goal of
what is being done is to learn something new or improve current understanding.

I place little value in being busy for the sake of being busy (there are times
when this is OK but they are fairly limited). An example would be if there is a
manual activity being repeatedly done, it should ideally be automated. Another
example might be if somebody has a desire to analyse some organisational data
from several data warehouses, it can be easy to just ask for all of it. If the
effort to do that is the same it isn't a problem. However, if the effort isn't
the same, the objective of the analysis needs to be more well defined. It might
be that not everything is required and the effort can be reduced. Asking
questions like this can also help to tease out the essence of the activity and
understand the value of it.

The question is, 'How do you maximise the work not done?'.

I think techniques to understand the answer to the question work best when
dealing with software as it is often relatively easy to figure out ways to
learn more about the problem in safe ways and ways that are very close to the
actual problem. The same is much harder to achieve in the physical world,
although it is possible to learn what people want.
[Desire paths (aka lines)](https://en.wikipedia.org/wiki/Desire_path) are a
good example of this.

With software, opportunities are much easier to come by. An example I read and
will always remember the moral of (if not the details) was about a company
selling something like bird cages (it doesn't really matter what it was).

The story goes along the lines of somebody wondered if
there was a market for bird cages in their home country. They knew there was a
big market in other countries but hadn't seen any sellers in their country. In
order to figure out if anybody was interested in buying bird cages they created
an advertisement on a search engine with a contact form, not really expecting
it to do much. Some short period of time later they were capturing a lot of
contacts so they knew there was a market and could afford to invest in it. At
this point the cost had been minimal and they had a database of people who were
wanting to buy a product they didn't have. A good position to be and much
better than having a load of stock with no customers. They got in touch with
the manufacturers and were able to get stock for their customers. There was a
lot of manual effort to start with but they had a business they were able to
make money from and grow.

I like this story as it epitomises figuring out a very low cost, low effort way
to learn if there was any demand from which a successful company was created.
Very much maximising the work not done (until it was required). It would have
been very different if the company had been setup, created a website for order
fulfilment, got the manufacturers and shipping sorted without any income or
knowledge whether there was a demand.

## You build it, you run it

I subscribe to the idea of 'if you build it, you run', from a
software product perspective (there are caveats to this and the context is all
important). It goes hand in hand with thinking about products as opposed to
projects and intimately ties two frequently separated stages of a product's
life cycle (development and operating) together. Doing so brings some keys
benefits such as:

* Consistency, an existing knowledge base and understanding of the
  history of the product
* A desire to make the product as good as possible as opposed to running
  somebody else's thing
* A much reduced chance of rework so it fits in with the other products the
  operations teams manages
* There isn't anybody else to point at when things break

These benefits all add up to providing a better product for the users. Which
isn't to say you can't have great products that are built and operated by
different teams of people but I believe there needs to be a clear lineage and
relationship between the two groups for the best experience. And it tends to be
easier to do that when it is the same team.

## Do not outsource your key competencies

Lots of organisations outsource work and there are lots of good reasons to do
so. When the work is mundane and not a reason why you are in business it makes
a lot of sense. It might be something like a bakery buying accounting software
or a plane maker employing a security contractor. This make sense, neither of
those businesses are outsourcing the reason they have a business.

It becomes odd when you hear about businesses outsourcing their own business.
For example, a business providing specialist recruitment services should not
be outsourcing recruitment services to external parties. If you are paying an
external entity to do your business you are losing out on all of the learning
you should be doing about your business. This is effectively paying somebody to
learn about what makes your business a business.

In most cases that isn't going to turn out so well. That might happen quickly
or it might be a slower decline where you are being put in a position where
your competitors, at least the ones who have been learning about the business
will be able to out manoeuvre you. Something you do not want that to happen.
