---
layout: post
title: Try Harder
---

{{ page.title }}
================

<p class="meta">Try harder</p>


Here is a pattern I've been seeing a lot.  We make a call and want to only
accept certain responses.


{% highlight python %}
def typical_func(tries=0):
    res = 'error'
    if tries < 4:
        res = random.choice(range(11))
        if res != 0:
            return typical_func(tries+1)
    return res
{% endhighlight %}

First question:  Why is this done recursively?   Seems like a job for iteration.
But you want it recursive?  OK.   Here are better recursive versions, with
shallower indentation.


{% highlight python %}
def better_recursive(tries=0):
    if tries >= 4:
        return 'error'
    res = random.choice(range(11))
    if res == 0:
        return res
    return typical_func(tries+1)


def br2(tries=0):
    if tries >= 4:
        return 'error'
    res = random.choice(range(11))
    return res if res == 0 else typical_func(tries+1)
{% endhighlight %}


The offensive thing about the recursive version is it introduces a new parameter
into the function.  Here is an iterative version.

{% highlight python %}
def maybe_better():
    tries=0
    while tries < 4:
        tries += 1
        res = random.choice(range(11))
        if res == 0:
            return res
    return 'error'
{% endhighlight %

But here's another idea.   The retry functionality is a completely separate
issue from the original problem.  It's really a shame that the function has to
take account of all this retry bookkeeping.   This looks like a job for a
decorator!


{% highlight python %}
{% endhighlight %


{% highlight python %}
{% endhighlight %

* about this
* that
* the other

{% highlight python linenos %}
def foo():
    print 'bar'

{% endhighlight %}


--

[Discuss RDD on Hacker News](http://news.ycombinator.com/item?id=1627246)
