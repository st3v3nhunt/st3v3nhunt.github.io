---
title: "📚 Using Architectural Decision Records"
date: "2022-07-10"
tags: ["adr", "architecture"]
categories: ["development"]
---

Decisions are made all of the time when developing software. Some decisions are
small and easy to change such as the name of a variable or whether to extract
some code into a separate class/function/module. Other decisions are larger and
more difficult to change such as which test framework to use, whether to use
JSON or XML or if a NoSQL database should be used in favour of a SQL database,
etc.

## Making decisions

When a decision is made, the person making it _should_ understand a number of
factors about the decision including the context within which it is being made,
the reason(s) for making it and what the potential impact or consequence(s) of
it will be. It is generally straightforward to communicate the reason(s) and
consequence(s) to other people, however, the context is less obvious as it is
often taken for granted that other people implicitly understand it. Often this
is not the case.

This is especially true if the team is large and/or working in
a fluid environment. There are other situations where context, and indeed the
other information pertaining to the decision is not available to learn from.
This can include when new people join the team or indeed your future self.

## ADRs

This is where
[ADRs](http://thinkrelevance.com/blog/2011/11/15/documenting-architecture-decisions)
come into play. An ADR or Architectural Decision Record is a way of recording
important decisions you want to record for others (including
your future self) so they can learn and help to understand why something
was done the way it was.

It is easy to review a software system and be critical of how it has been
implemented and provide suggestions about how this or that could be done
better. Doing this without the context as to why a particular approach has been
taken is much less valuable.

It is much more valuable to make suggestions that haven't been tried before
rather than suggesting the same thing again. Or recommending an approach
with an appreciation of how a similar approach didn't work previously.

If the person(s) responsible for making the decision(s) in the past is
available to explain why then some of this information will be able to be
communicated, however, people's memories are fallible.
Having a written record is vastly superior. This is a situation where ADRs
come into their own.

Another benefit or writing an ADR is to help the decision maker(s) more
thoroughly understand the rationale for the decision, the options available at
the time and the consequence(s) of making it. It really is very helpful to
capture the other options that were available including the reason(s) why these
were not chosen.

## MADRs

A more recent and more generalised version of an ADR exists, a
[MADR](https://adr.github.io/madr/) - Markdown Any Decision Records.

MADRs appear to have various forms (based on how much information is required
to capture the decision). There are examples for a
[short version](https://adr.github.io/madr/examples.html#short-version) and a
[long version](https://adr.github.io/madr/examples.html#long-version).

Some of the changes look really positive such as being explicit about the
`Considered Options` along with the consequences being split into `Positive
Consequences` and `Negative Consequences`. I can imagine this helps the author
to structure their thought process and ensure the decision is both considered
and information is not omitted from the written record.

I've not used MADRs but would consider them in the future.

## Creating and managing ADRs

### When to create an ADR

If you are using ADRs a couple of questions will inevitably crop up.

The first will be `When should I create an ADR?`. Inevitably, the answer is
`it depends`. The guidance I would give is, anything:

- your future self would ask why it was done this way
- you have been questioned about and had to explain
- that has been discussed and debated
- where there were several options to choose from
- that deviates from existing standards

Some examples:

- Using a 15 minute timeout for a magic link
- Using StandardJS rather than ESLint
- Making the code private rather than public
- Using C# rather than JavaScript
- Using Svelte rather than React

### How to manage ADRs

The second question is likely to be related to how ADRs should be managed. This
is especially pertinent when the decision impacts multiple code repositories,
a likely scenario when using microservices.

As above, the answer isn't necessarily straightforward as it depends on the
context of the team/project/organisation in which you are working.

ADRs should be co-located with the code where the decision has an impact.
This should always be the case. If this isn't happening, a lot of the
value provided by ADRs is lost. People working on the code might not even know
ADRs are being used in which case any new decisions are unlikely to be
recorded, and learnings from previous decisions are not available to provide
context to the team.

In situations where an ADR spans multiple repositories this might suggest the
decision is dealing with a standard. Ideally there are mechanisms for
recording standards outside of the repository, this might be at the project
or organisation level.

If the ADR is not a standard and thus will not be recorded elsewhere and is
applicable to multiple repositories I would suggest an ADR is added to each
impacted repository, ideally with a link to the related ADR(s) to aid in the
documentation.

## Why use an ADR rather than commit messages?

A good commit message should contain the
[reason for the change](https://blog.st3v3nhunt.me/posts/are-your-commit-messages-insightful/)
rather than simply recording what the change is. Therefore, you might
reasonably ask why commit messages shouldn't be used to record the information
being added to the ADR?

There are a number of reasons:

- Commit messages are much less visible than ADRs
- Commit messages are generally for small chunks of work and it is likely
  several commits would span what is covered by a single ADR
- Tooling exists to create websites out of ADRs, further increasing visibility
  and ease of use
