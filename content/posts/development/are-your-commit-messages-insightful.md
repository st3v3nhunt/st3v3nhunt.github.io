---
title: ":mag: Are your commit messages insightful?"
date: "2015-10-13"
tags: [ "commits", "development", "practices", "sourcecontrol" ]
categories: [ "development" ]
---

A good commit message is a hard thing to do.

Why do I say this? From my experience most of the commit messages are a
repetition of information contained in the commit itself. An example would be
something along the lines of where a change to the colour of a button was
required. Perhaps the button was changed from red to blue, the reason for the
change was due to user research showing blue was more enticing to the customer,
resulting in more clicks of the button (a good thing).

For this type of change I would not be surprised to see a commit message along
the lines of `button changed from red to blue`. Whilst this is not _untrue_ it
doesn't give your future self much to go on as to the reason for the change. It
also repeats information that can be gained by looking at the commit.

In my opinion, a more useful message would include the reason why the change
was made. Something like `blue button attracts more clicks`. If you or I were
to look back at the change in 6 months it becomes very clear why the button
colour was changed. This could prevent an arbitrary change of colour, possibly
reducing the number of clicks, from being made. I'm not sure the first message
would have provided that insight.

How do you make your commit messages provide value in the future? Is there a
recipe that can be followed?
