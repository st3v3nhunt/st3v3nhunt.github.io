---
title: "🔊 Communicating changes in PRs"
date: "2022-06-09"
tags: [ "commits", "guidance" ]
categories: [ "development" ]
---

When asking for a review of a pull request (PR) ensure there is suitable
context provided to the reviewer(s).

Probably the easiest way to do this is to add information to the description of
the PR. This way, anybody can see it and the information is retained for future
users.

On occasion there might be information not suitable to be made public. In this
situation, messages to the reviewer(s) via an external messaging system such as
Discord, Slack, Teams, etc. should be used. This might take the form of
providing the additional information in a channel or via direct messages to the
individual(s) who will be performing the review.

Using external messaging systems has the additional benefit of being able to
discuss the change in a private, (a)synchronous way rather than relying on the
email being sent with comments on from the Git provider. Relying on the Git
provider to send emails can break the flow and mean synchronous communication
isn't possible.

A downside to using external messaging systems is that potentially pertinent
information is not available to people who might want to be involved in the
reviewer but are not included in the other channels.

## Personal experience

In my experience, a mixture of providing base contextual information within the
PR's description is always useful. Along with additional information provided to
the reviewer(s) via the messaging system of choice.

I also typically use a messaging system to discuss details about potential
changes rather than having a conversation over PR comments. However, this does
vary if I think it would be useful to have the discussion in public forum where
I or others can refer back to in the future.
