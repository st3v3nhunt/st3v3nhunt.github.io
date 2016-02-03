---
layout: post
tags: [c#, development, razor]
title: Dashed html attribute in C Sharp view engine
---

How do you generate attributes for html elements that have a dash (`-`) in them through a C# view template engine while using object initialiser syntax?

Use an underscore (`_`) instead.

An example. In a Razor view using the `Html.ActionLink(...)` helper to create an anchor element with an attribute called `data-values` the code would be:

```csharp
@Html.ActionLink(
  "link text",
  "actionName",
  new { Model.Id },
  new { data_values = "some-value-for-the-data" })
```

Sourced from [Stackoverflow](https://stackoverflow.com/questions/9444805/how-to-specify-data-attributes-in-razor-e-g-data-externalid-23151-on-this/9444822#9444822)
