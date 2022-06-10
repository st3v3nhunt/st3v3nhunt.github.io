---
title: ":chart_with_downwards_trend: What lessons should one learn from the Gliffy outage?"
date: "2016-03-30"
tags: [ "development", "lessons", "sass" ]
categories: [ "development" ]
---

Ever since the recent lengthy and complete
[outage of Gliffy](http://support.gliffy.com/entries/98911057-RESOLVED-Gliffy-Online-System-Outage-),
I have been thinking about how I could (should that be a should?) protect
myself when working with SaaS. Everything is sorted now and Gliffy have a
[post](https://www.gliffy.com/blog/2016/03/25/turtle-and-the-hare/) explaining
a bit more detail on the outage. One of the takeaways from that being disaster
recovery plans should probably be practiced more often.

I tend to be quite trusting of SaaS and often come to the conclusion the people
running the services are better at running them and having disaster recovery
plans in place (and practiced) than I would be if I tried to implement some
form of backup. They also tend to be more invested in the continued success of
the service than I do as I'm guessing it pays some of their bills.
However, I increasingly think I’m probably on the wrong side of the fence on
this and I should be erring on the side of caution a bit more.

Of course, how trusting I am willing to be depends on what and how I’m using
the SaaS. If it is just a ‘plaything’ I can probably leave it as is and not
worry if the service goes down and never comes back. For example, I had a
handful of diagrams saved in Gliffy that I did not need access to during the
downtime and they mean so little to me that if I had never got them back I
wouldn't be particularly bothered. However, if I had needed them for a talk or
to look at or to hand in I'd have been pretty miffed.

This leads me to wonder if I should designate different levels of importance to
different SaaS. However, that would not be good if I at some time decided to
save something more important in a service that I had previously seen as less
important. And I don't want to have to remember each time I use a service what
level of importance I might have placed on it. So from the POV of making it
easy for myself I think having a single level of importance for everything
would make things easier. Then it is just a case of having to answer a single
question "Do I have a backup in place for this service"?

Which leads onto looking for the answer as to what a good backup solution might
be...
