---
layout: post
tags: [powershell, tips, agile, development]
modified: 2015-07-29
comments: true
---

A collection of Powershell snippets I have found useful.

* Set the title of the window:

{% highlight powershell %}
(Get-Host).UI.RawUI.WindowTitle = "New Window Title"
{% endhighlight %}

* Reload the path for the session ([source](http://stackoverflow.com/a/17794885/3205689)):
{% highlight powershell %}
$env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine")
{% endhighlight %}


* Delete all files/folders without confirmation messages:
{% highlight powershell %}
rm -r -force .\path\to\dir
{% endhighlight %}
