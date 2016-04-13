---
layout: post
tags: [development, ci, teamcity, gitlab]
comments: true
title: Create branch based NuGet packages in TeamCity
---

As I was reviewing the TeamCity build configuration I'd [setup](https://st3v3nhunt.github.io/teamcity-pipeline/) with my colleagues, it was pointed out every build was creating a new NuGet package. Not great when you consider every branch was triggering a build and most of those branches were not `master`.

## The problem with every branch

Generally it is not a good idea to have every branch generating a NuGet package when those branches are often feature branches i.e. code that is in the process of being reviewed but has not yet been merged into `master`. These were not changes we wanted to be published into the NuGet feed and made available to consumers by default.

As I was thinking about ways this could be solved I recognised  what I really wanted was a build step controlled by some (probably environment/execution context) variable. Looking around the Internet to see what other people did when faced with this situation I found a feature request ticket for exactly this - [Execute a build step based on a condition](https://youtrack.jetbrains.com/issue/TW-17939). The ticket is over 4.5 years old so whether the feature will be implemented remains to be seen (one would think not).

Thinking about why this seemingly innocuous feature might not have been implemented, it struck me that build pipelines should be all about procedural steps that produce the same outcome each and every time they are executed. This is what builds (no pun intended) trust in the process and allows people to rely on them. Adding conditional logic is adding something that might go wrong, and things often go wrong when you least want them to (and have forgotten about the condition even existing)!

## Possible solutions

In the ticket a number commenters share their workarounds.

* Some people create additional build configurations and use VCS triggers to control which branch goes through which build configuration.
* Others look to leverage the shell and environment variables to control what happens within a single build configuration.

Thinking about the implications of the two options I decided to use a PowerShell script to control the generation of the NuGet package. I chose this option primarily due to GitLab only supporting a single TeamCity build configuration and I wanted to maintain the integration between GitLab and TeamCity.

## NuGet creation via PowerShell

The PowerShell script I ended up with is:

<script src="https://gist.github.com/st3v3nhunt/48a8009c03608b3870596cdae0e09da7.js"></script>

The logic is straight forward enough, if the branch is determined to be the default one, create a package based on the build number e.g. `1.0.12`. If the branch is not default a [prerelease package](https://docs.nuget.org/create/versioning#user-content-prerelease-versions) will be created with the branch name appended to the build number e.g. `1.0.11-not-master`.

A convention the team I work in has is to have the branch name prepended with the word 'feature' e.g. `feature/new-thing`. NuGet does not support that convention for the version number due to the `/`. The script replaces all instances of `/` and replaces them with `-`.

Taking this approach allows all branch builds to be visible in the NuGet feed but only those built from `master` are not marked as prerelease. This means as we develop the package we can select specific prerelease versions to test before merging them into `master`, should we wish.
