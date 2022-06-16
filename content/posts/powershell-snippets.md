---
title: "🔌 Powershell snippets"
date: "2015-07-15"
modified: "2016-02-18"
tags: [ "agile", "powershell", "tips" ]
categories: [ "development" ]
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

* List all environment variables with `Get-ChildItem` and its' aliases:

```powershell
Get-ChildItem Env:
gci Env:
dir Env:
ls Env:
```

* Get specific environment variable using the `Path` as an example. The first
  option returns just the value whereas the second returns it in a table
  format:

```powershell
$Env:Path
gci Env:Path
```

* Set specific environment variable:

```powershell
$env:Path = 'new value goes here'
$Env:Path = 'new value goes here'
```
