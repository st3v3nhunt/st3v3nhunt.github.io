---
layout: post
tags: [powershell, tips, agile, development]
modified: 2015-07-29
comments: true
---

A collection of Powershell snippets I have found useful.

* Set the title of the window:

```powershell
(Get-Host).UI.RawUI.WindowTitle = "New Window Title"
```

* Reload the path for the session ([source](http://stackoverflow.com/a/17794885/3205689)):

```powershell
$env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine")
```


* Delete all files/folders without confirmation messages:

```powershell
rm -r -force .\path\to\dir
```
