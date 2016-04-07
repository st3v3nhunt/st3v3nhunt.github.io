---
layout: post
tags: [development, ci, teamcity, gitlab]
comments: true
---

It has been a while since I setup a build configuration in TeamCity. I thought I would record what I did this time around.

First up, a bit of  background - the solution is a pretty simple .Net library. It uses NuGet to fetch some dependencies and I want to package the code up as a NuGet package. I want to make it available in the TeamCity NuGet feed.

The source code is hosted in a GitLab instance. I wanted to make use of the GitLab and TeamCity integration so I would be able to see how an MR got on with CI. This would save people time potentially looking at an MR that doesn't even pass CI.

## Build Steps

There are 6 build steps:

1. Restore [NuGet packages](https://confluence.jetbrains.com/display/TCD9/NuGet+Installer)
2. Build with [Visual Studio](https://confluence.jetbrains.com/pages/viewpage.action?pageId=74847254) - Clean & build the solution in release configuration
3. Run [Duplicates Finder](https://confluence.jetbrains.com/pages/viewpage.action?pageId=74847275):
  * Include `**/*.cs`
  * Exclude `**/*.Tests` and `**/Properties`
4. Run [FxCop](https://confluence.jetbrains.com/display/TCD9/FxCop):
  * Include `**/bin/Release/*.dll`
  * Exclude `**Tests**`
5. Run [NUnit](https://confluence.jetbrains.com/display/TCD9/NUnit) tests.
  * Include [JetBrains dotCover](https://confluence.jetbrains.com/display/TCD9/JetBrains+dotCover) code coverage
6. [Package](https://confluence.jetbrains.com/display/TCD9/NuGet+Pack) the NuGet Packages. The packages are only made available on the TeamCity feed so there is no [Nuget Publish](https://confluence.jetbrains.com/display/TCD9/NuGet+Publish) step

## Integration of CI and VCS

I do love an automated check. And those checks are even better when they are done for all MRs before anybody has spent any time eyeballing them. In order to get TeamCity and GitLab to communicate together I did this:

* In GitLab I went into the project's Settings `-->` Services `-->` JetBrains TeamCity CI screen. I completed the form for the TeamCity server I wanted to integrate with.
* As instructed on the form in GitLab I went to TeamCity and set the Build number format to `%build.vcs.number%`.

That is it. Now all branches trigger a build in TeamCity and MRs have the integrated CI status check.

## CI failure conditions

Part of the power of CI is being able to fail the build on pre-defined conditions. For this pipeline I have additional failure conditions as well as the standard of any failing tests and non-zero exit codes. The additional failure conditions are:

* Fail build if build duration (secs) is different by at least 50% compared to the last successful build
* Fail build if artifacts size (bytes) is different by at least 50% compared to the last successful build
* Fail build if number of ignored tests is more than 0
* Fail build if number of tests is less by at least 20% compared to the last successful build

Some of those criteria are probably a little on the 'kind' side and will not be suitable for all projects or at all times of their life. For example, having the number of tests reduce by 20% in a mature project is almost definitely far too many, as is the build duration and artifacts criteria. On the other hand, if that project is near to it infancy the build duration might well double if a new suite of tests was introduced.

For very young projects it is probably a good idea to disable some of the advanced failure conditions until such a time when the project has some history and predictability.
