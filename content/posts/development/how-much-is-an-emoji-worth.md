---
title: ":dollar: How much is an emoji worth"
date: "2015-10-13"
tags: [ "agile", "development", "emoji", "git" ]
categories: [ "development" ]
---

I have written a bit about how to make your commit messages more
[insightful](are-your-commit-messages-insightful/).

If the idiom
[a picture is worth a thousand words](https://en.wikipedia.org/wiki/Ae_picture_is_worth_a_thousand_words)
is true, perhaps using emoji to add an extra level of information to your
commit messages is a good idea? Even if it is not, I would recommend adding
emoji to commit messages.

Emoji add some :sparkles: to your commits. Looking back over the history has
never been so colourful. A lot of source control web interfaces support emoji
so having an emoji on every commit can brighten up the code home page of your
project, possibly making it more attractive to potential contributors. And
everybody likes the idea of more people working on their project, right?

## How do I choose an appropriate emoji?

Given there are [so many](http://emojipedia.org/faq/) emoji, how do you know
which to use?

Whilst there are no 'official' rules about when and how to use emoji I would
like to propose the following guidance (perhaps this could be the first
officially recognised rule? `:wink:`):

* Only :one: :boom: allowed per repository. It can only be the very first
  commit, if not used for the first commit it is not permitted within the
  repository. Should a :boom: be used within any subsequent message the entire
  commit shall be rejected during the pull/merge request process.

It was once said to me that the choice of the emoji should be based on how it
made one feel, the emotional state of the commit made real via emoji. I find
this to be a good place to start but occasionally tricky. When this approach
fails I fall back to looking for an emoji to represent what has changed or
ideally, why the change was made.

An example would be when finishing up a feature, knowing that commit will be
pushed to the production environment. The `:shipit:` emoji is apt or a bug fix
the generic `:bug:` can suffice.

---

What do you think to adding emoji to your commits? Is this a practice you
follow and do you have any guidance for the uninitiated?
