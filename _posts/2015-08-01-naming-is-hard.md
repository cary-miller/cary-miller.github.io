---
layout: post
title: Naming is hard
---

{{ page.title }}
================

keywords:  programming, naming

<p class="meta">naming</p>

After programming for several years I conclude that naming is
grossly under-appreciated.    I begin to look around and see
others with the same thought.   The subject of naming brings out the
fanatic in coders so I try to keep Alistair Cockburn's
[Oath of Non-Allegience][oath] in mind.

> I promise not to exclude from consideration any idea based on its source, but
> to consider ideas across schools and heritages in order to find the ones that
> best suit the current situation.


The [c2][] web site is loaded with interesting programming ideas,
such as [Good Variable Names][].  It's
also got a lot of rabbit holes relating to bad names.   Another trove, with a
functional (clojure) orientation, is [lispcast][].   This
guy advocates dealing with the 
[naming issue by avoidance][avoid].   
His main point is to avoid naming things by

- inlining functions
- etc


Inlining a function results in an anonymous function which now requires a comment.
show examples.
Of course there's a time and a place for everything.


Another take on it from [codemesh][]

> Names are the one and only tool you have to explain what a variable does
> in every place it appears, without having to scatter comments everywhere.

- 


One of the good points made by lispcast is a rant on style vs substance.
which leads to ...


[something manager]: http://blog.codinghorror.com/i-shall-call-it-somethingmanager/
[lispcast]: http://www.lispcast.com/
[avoid]: http://www.lispcast.com/avoid-naming-at-all-costs
[codemesh]: www.codemesh.io/static/upload/.../141537864327479namingthings.pdf)
[c2]: http://c2.com
[good variable names]: http://c2.com/cgi/wiki?GoodVariableNames
[oath]: http://alistair.cockburn.us/Oath+of+Non-Allegiance
[id]: url "optional title"
[id]: url "optional title"

--
