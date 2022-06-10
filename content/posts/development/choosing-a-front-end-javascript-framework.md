---
title: ":triangular_ruler: Choosing a frontend JavaScript framework"
date: "2015-09-09"
tags: [ "angularjs", "development", "frontend", "javascript" ]
categories: [ "development" ]
---

The majority of my coding time is spent in the back-end, so to speak. Mostly
within a Microsoft environment. When an opportunity arises to discard the
shackles of Visual Studio I figuratively leap at the chance.

Lucky for me, just such an opportunity presented itself in the not so distant
past. It wasn't going to be all <s>sweetness</s>
[Sublime Text](http://www.sublimetext.com/) and <s>roses</s>
[Chrome DevTools](https://developer.chrome.com/devtools) but enough to whet the
appetite for something less, well, less...restrictive (mostly in the sense of
the systems that have been built as opposed to the tooling).

## Best practices

I haven't done too much front-end development over the past couple of years so
I delved into the depths of my memory (unpleasant) and pulled out what I
thought were good practices for writing JavaScript. Things like:

* [The revealing module pattern](http://addyosmani.com/resources/essentialjsdesignpatterns/book/#revealingmodulepatternjavascript)
* [Google's Code Style](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml)
* [JSHint](http://jshint.com/)
* [Immediately-invoked function expression](http://benalman.com/news/2010/11/immediately-invoked-function-expression/)

As it happens, these are still good things to be doing. Check out
[JavaScript The Right Way](http://jstherightway.org/) for more comprehensive
information.

## DOM manipulation

When it came to manipulating the DOM I instinctively turned to what I had used
in the past - [JQuery](https://jquery.com/). Chosen as much because I had
experience with JQuery as it was because I didn't have a choice.

The work was completed and I was quite happy with the relatively minimal DOM
manipulation I had managed (choosing to show/hide pre-built elements within the
page, as opposed to building lots of stuff within JavaScript). However, I was
left feeling disappointed the code was not better.

I wanted more. I knew of some front-end JavaScript frameworks (amongst the many
hundreds of others):

* [AngularJS](https://angularjs.org/)
* [Backbone.js](http://backbonejs.org/)
* [Ember.js](http://emberjs.com/)
* [knockout.js](http://knockoutjs.com/)

I was confident I needed to embrace one of them. This would make both myself
and the code I produce better than the current situation.

## Choices, choices, choices

But which one to try? Sure, I could try them all (and I probably should),
however, I wanted to know which to try first.

Colleagues consulted, Google searched, GitHub's
[front-end JavaScript frameworks](https://github.com/showcases/front-end-javascript-frameworks)
showcase reviewed. There was a clear leader - AngularJS.

## Decision made - AngularJS it is

Why? Well, it seems to be The Framework<sup>&copy;</sup> all the Cool
Kids<sup>&copy;</sup> are using. It's backed by Google. Using some (admittedly
fairly arbitrary) comparisons between the frameworks (all correct at the time
of writing) it comes out as a clear leader.

### GitHub Stars:

* 42,311 for [AngularJS](https://github.com/angular/angular.js)
* 22,886 for [Backbone.js](https://github.com/jashkenas/backbone)
* 14,693 for [Ember.js](https://github.com/emberjs/ember.js)
* 6,705 for [knockout.js](https://github.com/knockout/knockout)

### Questions tagged in [Stackoverflow](http://stackoverflow.com/):

* AngularJS - [119,314](http://stackoverflow.com/questions/tagged/angularjs)
* Backbone.js - [18,622](http://stackoverflow.com/questions/tagged/backbone.js)
* Ember.js - [16,546](http://stackoverflow.com/questions/tagged/ember.js)
* Knockout.js - [14,490](http://stackoverflow.com/questions/tagged/knockout.js)

### [Google searches over time](https://trends.google.com/trends/explore?geo=GB&q=angularjs,emberjs,backbonejs,knockoutjs)
