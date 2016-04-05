---
layout: post
tags: [development, git, gitlab, github]
comments: true
---

I really enjoy introducing people to Git. Pretty much without fail they see how much better their development work-flow can be and find their work more enjoyable as a result. This is especially true if they are coming from a TFS background. See how I work with [Git and TFS](https://st3v3nhunt.github.io/how-i-work-with-git-and-tfs/).
However, with pleasure comes pain. For Git, that pain is in getting over the learning curve. The size and steepness of the curve varies depending on previous experience of [Version Control Systems](https://en.wikipedia.org/wiki/List_of_version_control_software).
In my experience, TFS does not provide a good base knowledge to work from as it tries to hide as much as possible from the user. Clearly Git is doing a lot for you too but the way it works is more exposed. For example, even the most basic of things like adding files into the index can seem strange to a TFS user.

Each time I introduce people to Git I cover most of the same things. I've used crib sheets in the past but for the most recent round of introductions I thought I would write a post about it. This is that post!

## Why use Git?

I should really do a post specifically explaining the reasons I like to use Git. For the sake of brevity, these are the [official reasons](https://git-scm.com/about).

## Branch name conventions

I find it useful to have some conventions for the name of branches that will be pushed to the remote repository. I tend to use:

* feature/descriptive-name-of-feature
* fix/descriptive-name-of-fix

Naming conventions makes having specific things happening downstream easy e.g. deploy any and only feature branches to a brand new test environment. I wouldn't necessarily want to do that for a fix branch, perhaps that would be deployed over the top of the existing environment.
Having known reserved branch names also means people are free to push branches with non-reserved names for their own purposes e.g. backup or sharing.

## Commit message conventions

I've previously written about how I think [emojis add](https://st3v3nhunt.github.io/how-much-is-an-emoji-worth/) to the information contained within a commit message. And how to [provide insight](https://st3v3nhunt.github.io/are-your-commit-messages-insightful/) into the change being made, as opposed to simply regurgitating the change being made.

In addition to the points above I like to have the commit message adhere to the convention of starting with an emoji followed by a relatively short and succinct message. There are a number of good posts discussing this subject in detail, [On commit messages](http://who-t.blogspot.co.uk/2009/12/on-commit-messages.html) and [A Note About Git Commit Messages](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html) to name two.
To summarise, the commit message should ideally have:

* An emoji to start with!
* A first line, the summary message, length of ~50 characters
* A blank line after the summary, when there are additional comment lines
* Additional comment lines not exceed ~72 characters

## Commit conventions

Good commits should generally:

* Include a single thing i.e. renaming and fixing are different things and do not belong in the same commit
* Be as small as possible. If you are ever tempted to just do that really small extra change in a commit - don't. Finish up what you are doing and do the other thing in another commit. You (and your colleagues) will thank yourself when you need to see what changed when _that_ bug was introduced!

## Git aliases

I've got another [post](https://st3v3nhunt.github.io/git-aliases/) on git aliases and how to share them.

## Branch protection

I have found out the hard way, protecting branches is a very good idea. No force pushing to master (or any other shared branch) is an absolute necessity for your sanity.

## Merge/Pull\* request assignments

When an MR is created you are asked a number of questions. One of them being who you would like to assign it too. The question does not need to be answered immediately, or ever in fact. However, it is a good idea to have the team know how this works in order to avoid the [whose job is it anyway](https://gist.github.com/st3v3nhunt/f71a36f697b3392310fffeead01541b7) problem.

Working in a small team the rule I usually work by is to not have the MR creator assign anybody. The first person to get to the MR assigns them self. The problem of nobody assigning themselves can happen but when everybody knows each other in the team and there is good communication about what people are doing this tends to not be the case. It also allows the people who are free to get to the MR rather than possibly interrupting people in the middle of something else.

\* When I use the terms merge request (MR) and pull request (PR) I so do interchangeably.

## Delete merged branches

Good housekeeping is to remove branches once they have been merged. When using lots of branches the number of merged branches hanging around can get a bit out of hand. Removing them as soon as they have been merged solves this problem.

## Keep a useful history

As has been discussed above, keeping commits small and focused is a good idea. Following this principle is a great way of achieving a clean and more importantly, a useful history.

MRs introduce an opportunity for that guidance to be difficult to follow. For example, if there have been several small commits created in order to build a feature - when that feature comes to be merged, should those commits be retained or should they be squashed into a single commit? Prior to [April 1st 2016](https://github.com/blog/2141-squash-your-commits) the only option on GitHub was merge commits.
A merge commit retains the details of the history of the branch unless those commits had been squashed by the branch owner. I used to think having the branch history squashed was a good idea as it would be a clean entry. However, I now think the benefit of having the detailed commit history and how the feature was built is more valuable. That is not to say squashing commits that are not 'complete' should not be done - they should be squashed if they provide no value.

In summary, I think having both merge commits and [squash merging](https://help.github.com/articles/about-pull-request-merge-squashing/) options available on a GitHub repository is good.

The most important thing to keep in mind is that commits should provide value to the code base and by following the guidance here you will be on the way to doing so.
