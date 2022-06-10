---
title: ":tada: TeamCity Pipeline - iteration two"
date: "2016-04-28"
tags: [ "ci", "development", "gitlab", "teamcity" ]
categories: [ "development" ]
---

Now I have had the [TeamCity build
pipeline](../teamcity-pipeline/) running for a while
I have had chance to review how it works. I have made a number of changes which
I have summarised, along with the reasoning below.

## Additional build step

Originally there were 6 build steps, now there are 7.

The new build step is executed as the first step and its purpose is to prevent
the build from continuing if a
[History Build](https://confluence.jetbrains.com/display/TCD9/History+Build) is
detected. The way I detect a history build is to check the SHA-1 of the default
branch and compare it to the SHA-1 being built.

This is not quite correct as far as the TeamCity definition goes for a history
build but it works in order to prevent old code being packaged into the NuGet
packages. This was happening whenever a branch was deleted as it was merged
into the default branch.

There is a check to make sure the build is not for the default branch so the
build will only be stopped when the code being built is the same as that in the
default branch but it is not the default branch that is being built. This has
the impact of branches that contain the same code as the default branch will
not be built, however, we felt the trade off is worth it.

The script used is ostensibly the same as this:

```powershell { linenos=true }
<#
Params:
$current_build_sha = "%build.vcs.number%"
$root_branch       = "%vcsroot.branch%"
$is_default_branch = "%teamcity.build.branch.is_default%"
$vcs_root_url      = "%GIT_ROOT_URL%"
$private_token     = "%GIT_PRIVATE_TOKEN%"
e.g. CheckForHistoryBuild.ps1 "%build.vcs.number%" "%vcsroot.branch%" "%teamcity.build.branch.is_default%" "%GIT_ROOT_URL%" "%GIT_PRIVATE_TOKEN%"
#>
param([String]$current_build_sha, [String]$root_branch, [String]$is_default_branch, [String]$vcsroot_url, [String]$private_token)

If ($is_default_branch -eq $true)
{
  Write-Host "Branch is default. Pipeline continuing..."
  exit 0
}

Write-Host "Get SHA-1 of the project's default branch ($default_branch_name) in order to compare to this build's SHA-1"
Write-Host "If they are the same the build will not be continued"
Write-Host "This is due to the build being a History Build (https://confluence.jetbrains.com/display/TCD9/History+Build)"
Write-Host "And history builds create NuGet packages with old code"

$default_branch_name = ($root_branch -split "/")[-1]
$api_url = "https://$vcsroot_url/api/v3/projects/55/repository/branches/$default_branch_name`?private_token=$private_token
$default_branch_api_response = Invoke-RestMethod $api_url
$default_branch_sha = $default_branch_api_response.commit.id

Write-Host "Call API @ $api_url"
Write-Host "Default branch name: $default_branch_name"
Write-Host "Master branch SHA-1: $default_branch_sha"
Write-Host "Current branch SHA-1: $current_build_sha"

If ($default_branch_sha -eq $current_build_sha)
{
  Write-Host "History build detected. Stopping pipeline..."
  exit 1
}
Else
{
  Write-Host "New build. Pipeline continuing..."
}
```

I have noticed the call out to the GitLab API is failing quite frequently. I
will looking into making it more robust in the future but it can wait for the
time being seen as the worst thing that happens is the history builds are not
detected. Hardly ideal.

## Rewritten NuGet package step

I have rewritten one of the original steps which I have already written about
regarding the creation of the
[NuGet packages](../branch-based-nuget-packages-in-teacmity/).
Since then I have made more changes to the script. The changes are mostly due
to it now being a standalone script and not source code saved in TeamCity. The
other changes are that a datetime stamp is no longer appended to the package
version as it isn't necessary, the pattern `-prerelease` is sufficient to
indicate a
[pre-release NuGet package](https://docs.nuget.org/create/versioning#user-content-creating-prerelease-packages).
The final change being to ignore errors during the deletion of the output
directory.
The new script is:

```powershell { linenos=true }
<#
Params:
$working_dir = "%teamcity.build.workingDir%"
$nuget_packages_dir = "%Generated nuget packages directory%"
$is_default_branch = "%teamcity.build.branch.is_default%"
$build_counter = "%build.counter%"
e.g. CreateNuGetPackages.ps1 "%teamcity.build.workingDir%" "%Generated nuget packages directory%" "%teamcity.build.branch.is_default%" "%build.counter%"
#>
param([String]$working_dir, [String]$nuget_packages_dir, [String]$is_default_branch, [String]$build_counter)

$output_dir = "$working_dir\$nuget_packages_dir"
$properties = "Configuration=Release"

Write-Host "Default branch detected: $is_default_branch"
Write-Host "Build counter: $build_counter"

Write-Host "Cleaning output directory: $output_dir"
rm "$output_dir\*" -Recurse -ErrorAction Ignore

If ($is_default_branch -eq $true)
{
  Write-Host "Package is versioned as release."
  $package_version = "1.0.$build_counter"
}
Else
{
  Write-Host "Package versioned as pre-release."
  $package_version = "1.0.$build_counter-prerelease"
}

..\..\tools\NuGet.CommandLine.DEFAULT.nupkg\tools\NuGet.exe pack $working_dir\MySolution\MySolution.csproj -OutputDirectory $output_dir -Version $package_version -Properties $properties -IncludeReferencedProjects
```

## Moved PowerShell script out of TeamCity

I was saving the PowerShell script directly in TeamCity but have moved the code
into a file and added it to the code repository.  I find having the script
alongside the code is a *much* better option, some of those reasons being:

* Anybody with access to the code has access to the build script (which is
  often different to those with access to the build configuration)
* The script is fully versioned
* The same scrutiny as the rest of the code gets is applied to the script
* Changes to the script are applicable only to the branch where those changes
  are rather than everything that runs through the build configuration - this
  is perhaps the most important reason

In the future I would go straight to having the build configuration reference a
script within the code base as the transition from one to the other is tricky.
Mostly involved with getting the script to work properly for the first time
whilst all builds are running, some of which do not have the build script in
the repo.


## Updated failure conditions

I started with four failure conditions and reduced that to three, of which only
two are from the original four.

The two I have disabled are the build duration and the artifact size. The
reason being, both were failing builds that were perfectly OK. I thought this
might be the case in the early days of the project as the code can and indeed
does change quite significantly from build to build.

The new failure condition goes hand in hand with the script to stop the build
when a history build is detected. The condition is triggered when the build log
contains some text that is output via the build script when the build has been
identified as one to be stopped.


## More changes?

For the time being those are the changes that have been made. As and when there
are more I will update this post or create a new one.
