---
title: DIY Git remotes
date: "2016-04-12"
tags: [ "development", "git", "tfs", "vcs", "ways-of-working" ]
categories: [ "development" ]
---

## Working with a non-cloud hosted Git remote

I often work in environments where the code is centrally stored in TFS. And as
I hate, HATE, **HATE** TFS I have to find other ways to interact with the VCS
to keep my sanity. [GitTFS](http://git-tfs.com/) to the rescue. I've written
about this [before](../how-i-work-with-git-and-tfs/).

I have a number of colleagues who feel the same way about TFS but until
recently we were happy to use the shelveset feature to do code reviews.
However, after a period of time doing 'proper' reviews in
[GitHub](https://github.com/) and [GitLab](https://gitlab.com/) one of my
colleagues decided enough was enough and we should do a more Git based code
review. I was up for doing that and immediately thought we should get the code
into our internal GitLab instance. They didn't want to do that and instead
preferred to use their own machine as the remote host. Rather than go into the
details of why we decided this was OK I'd like to cover the details of the work
flow.

## Local network shared Git repo work flow

The following describes how to work with a 'local' (local network share) remote
Git repo. This allows a team of developers working with GitTFS to implement a
code review system in Git where it is not possible to make changes to the
server based TFS system.

### Create network share

On a machine that is accessible by all members of the team a network share
needs to be created. This network share should contain the git repo that has
been created by GitTFS from the TFS source.

In the following example the network share machine is `WORKSRV_001` and the
location of the GitTFS repo is `C:\code\my-project`

The following commands should be run on a machine that is not where the network
share is (although this doesn't necessarily matter).

### Get the repo

If the directory where the commands are being run is already a Git repo (as it
was in my case) add a new remote:
`git remote add WORKSRV_001 //WORKSRV_001/C$/code/my-project`

Followed by a check out of the `master` branch:
`git cob WORKSRV_001/master WORKSRV_001/master `

If the directory is not a Git repo, clone it:
`git clone //WORKSRV_001/C$/code/my-project`

### Checkout the branch to review

When your colleague informs you there is a branch available for review, that
branch needs to be checked out locally so it can be reviewed.
`git cob review/<branch-name> WORKSRV_001/<branch-name>`

Follow your normal review process and remember to include checking the latest
code changes recorded in TFS are contained in the review branch.

### Merge the reviewed branch into a copy of master

Once the branch has been reviewed it can be merged into a copy of `master`. The
reason for merging into a copy of `master` is because the remote is somebodies'
local Git repo and we don't want to go messing with it!
`git co WORKSRV_001/master`
`git cob reviewed/<pull-request-description>`

When the copy of master is checked out the merge of the reviewed branch can
occur. This is done by creating a merge commit (the default behaviour of GitHub
and GitLab). To create a merge commit use the following options:

* no fast forward with `--no-ff`
* add a message with `-m "my commit message"`
* include the previous commit messages with `--log`

`git merge --no-ff -m "<message>" --log review/<branch-name>`

### Check into TFS

The reviewed and merged branch should now exist on the network shared Git repo.
The person whose machine hosts the network share needs to be informed of the
branch and that it should be pushed to TFS.

The push to TFS involves using GitTFS to check-in the changes:
`git-tfs checkin -m "<message here>"`

Hopefully no additional changes have been made to TFS during the review
process. If there are changes, the pusher will need to rebase the reviewed
branch against the latest changes (or ask one of the people involved in the
reviewed branch to do it) prior to checking it in.
