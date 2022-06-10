---
title: Create branch based NuGet packages in TeamCity
date: "2016-04-13"
modified: "2016-04-18"
tags: [ "ci", "development", "gitlab", "teamcity" ]
categories: [ "development" ]
---

As I was reviewing the TeamCity build configuration I'd
[setup](../teamcity-pipeline/) with my colleagues, it
was pointed out every build was creating a new NuGet package. Not great when
you consider every branch was triggering a build and most of those branches
were not `master`.

## The problem with every branch

Generally it is not a good idea to have every branch generating a NuGet package
when those branches are often feature branches i.e. code that is in the process
of being reviewed but has not yet been merged into `master`. These were not
changes we wanted to be published into the NuGet feed and made available to
consumers by default.

As I was thinking about ways this could be solved I recognised  what I really
wanted was a build step controlled by some (probably environment/execution
context) variable. Looking around the Internet to see what other people did
when faced with this situation I found a feature request ticket for exactly
this -
[Execute a build step based on a condition](https://youtrack.jetbrains.com/issue/TW-17939).
The ticket is over 4.5 years old so whether the feature will be implemented
remains to be seen (one would think not).

Thinking about why this seemingly innocuous feature might not have been
implemented, it struck me that build pipelines should be all about procedural
steps that produce the same outcome each and every time they are executed. This
is what builds (no pun intended) trust in the process and allows people to rely
on them. Adding conditional logic is adding something that might go wrong, and
things often go wrong when you least want them to (and have forgotten about the
condition even existing)!

## Possible solutions

In the ticket a number of commenters share their workarounds.

* Some people create additional build configurations and use VCS triggers to
  control which branch goes through which build configuration.
* Others look to leverage the shell and environment variables to control what
  happens within a single build configuration.

Thinking about the implications of the two options I decided to use a
PowerShell script to control the generation of the NuGet package. I chose this
option primarily due to GitLab only supporting a single TeamCity build
configuration and I wanted to maintain the integration between GitLab and
TeamCity.

## NuGet creation via PowerShell

The PowerShell script I ended up with is:

```powershell { linenos=true }
$output_dir = "%teamcity.build.workingDir%\%Generated nuget packages directory%"
$properties = "Configuration=Release"

Write-Host "Cleaning output directory: $output_dir"
rm "$output_dir\*" -recurse

If ("%teamcity.build.branch.is_default%" -eq $true)
{
  Write-Host "Package is versioned as release for branch: %teamcity.build.branch%"
  $package_version = "1.0.%build.counter%"
}
Else
{
  Write-Host "Package versioned as pre-release for branch: %teamcity.build.branch%"
  $patch_name = Get-Date -UFormat %%Y%%m%%d%%H%%M%%S
  $package_version = "1.0.%build.counter%-pre$patch_name"
}

..\..\tools\NuGet.CommandLine.DEFAULT.nupkg\tools\NuGet.exe pack %teamcity.build.workingDir%\MySolution\MySolution.csproj -OutputDirectory $output_dir -Version $package_version -Properties $properties -IncludeReferencedProjects
```

The logic is straight forward enough, if the branch is determined to be the
default one, create a package based on the build number e.g. `1.0.12`. If the
branch is not default, a
[pre-release version](https://docs.nuget.org/create/versioning#user-content-prerelease-versions)
will be created with the date and time the package was created e.g.
`1.0.11-pre20160418093024`. The reason for prepending the time stamp with `pre`
is to make the version number valid due to the pre-release section not able to
be purely numeric. Another change I had to make to the way I was originally
going to set the pre-release section (based on branch name) was due to the
length limitation of 20 characters max. The time stamp is a fixed length, until
we get to the year 10,000 AD at least.

Taking this approach allows all branch builds to be visible in the NuGet feed
but only those built from `master` are not marked as pre-release. This means as
we develop the package we can select specific pre-release versions to test
before merging them into `master`, should we wish.
