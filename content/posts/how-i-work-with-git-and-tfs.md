---
title: "😕 How I work with Git and TFS"
date: "2016-03-29"
tags: [ "development", "git", "gittfs", "tfs" ]
categories: [ "development" ]
---

This post has been one I've been meaning to write for months and months.
Finally, I've got round to it! This does mean specifics are going to be few and
far between...

**TL;DR:** Use [git-tfs](http://git-tfs.com/) as a bridge between the awful TFS
and the awesome Git.

I work in an organisation where the majority of the code is stored in
[TFS](https://msdn.microsoft.com/en-us/library/ms181237.aspx). I came from a
background where I used [Subversion](https://subversion.apache.org/). As soon
as I started to use TFS I hated it. I can't remember the full list of reasons
why I had such a strong dislike to it (other than because it was different 😉)
beyond the fact:

* Using it outside of Visual Studio was (probably still is) a very bad idea.
* The connected mode is a real nuisance when working with other people in the
  same area of the code.
* The way files were all read only.
* Locked workspaces.

These points probably all boil down to the always connected mode and that might
have changed since I stopped using it...I gave up using TFS directly almost
immediately after having first been exposed to it.

My first foray into hiding the awfulness of TFS was to use a Git to TFS bridge
called [Git-TF](https://gittf.codeplex.com/). I used this for several months
before I found there were some short-comings with it, that, at the time I was
unable to work around. I forget exactly what they were but I have a feeling the
ability to deal with files names over 256 characters in length might have had
something to do with it.

On the lookout for an alternative I came across [git-tfs](http://git-tfs.com/)
which I still use to this day. I have found git-tfs to be an invaluable
companion ever-since, even if the file length problem still exists. Fortunately
it is easily worked around with the
[`--workspace=`](https://github.com/git-tfs/git-tfs/blob/master/doc/commands/clone.md#set-a-custom-tfs-workspace-directory)
option.

Another niggle, which is nothing to do with how git-tfs works but is a result
of the structure of the code in the TFS repo is how I need to clone multiple
directories within a number of repos in order to have some semblance of
separation in how the code lives on my development machine. Add to that the way
branching is done and
[`quick-clone`](https://github.com/git-tfs/git-tfs/blob/master/doc/commands/quick-clone.md)
has become one of my favourite commands!

The final piece to the way I work with TFS puzzle is using [TFS
Sidekicks](http://www.attrice.info/cm/tfs/index.htm). I use this to do things I
could do with the git-tfs but am too lazy to do such as a quick visual check on
the history of the repo or, and this is its' main use, to view other people's
shelvesets.
