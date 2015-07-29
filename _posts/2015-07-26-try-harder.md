---
layout: post
title: Try Harder
---

{{ page.title }}
================

keywords:  python decorator "separation of concerns"

<p class="meta">repeat until satisfied</p>


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
into the function, strictly for retry-tracking.  Here is an iterative version.

{% highlight python %}
def maybe_better():
    tries=0
    while tries < 4:
        tries += 1
        res = random.choice(range(11))
        if res == 0:
            return res
    return 'error'
{% endhighlight %}

But these are just marginal improvements.   The function should not have to
think about retries.
Here's another idea.   The retry functionality is a completely separate
issue from the original problem.  It's really a shame that the function has to
take account of all this retry bookkeeping.   Wouldn't it be nice to define the
function this way:

{% highlight python %}
def best():
    return random.choice(range(11))
{% endhighlight %}

Good news!   It can be done.  This looks like a job for a decorator!


{% highlight python %}
def repeat_until_return_value_in(good_results, max_tries=5):
    def outer(func):
        @functools.wraps(func)
        def inner(*pos, **kw):
            i = 0
            while i < max_tries:
                i += 1
                res = func(*pos, **kw)
                if res in good_results:
                    return res
            return 'error'
        return inner
    return outer
{% endhighlight %}

This decorator takes care of the tedious but mandatory result-checking.   The
base function no longer has to worry about such things.   It just does its job
and goes merrily on its way.   


{% highlight python %}
@repeat_until_return_value_in((0,))
def better():
    return random.choice(range(11))


@repeat_until_return_value_in((0, 7, 9), max_tries=3)
def also_better():
    return random.choice(range(11))


@repeat_until_return_value_in((2, 22,), max_tries=7)
def another_better():
    return random.choice(range(11))
{% endhighlight %}

More to the story.   The original problem is usually in the form of a web
request and the acceptance trigger is the response status code.   So here is a
simulation of that scenario, with mocked-up Response objects.


{% highlight python %}
def repeat_until_status_code_in(good_codes, max_tries=5): 
    def outer(func):
        @functools.wraps(func)
        def inner(*pos, **kw):
            i = 0
            while i < max_tries:
                i += 1
                response = func(*pos, **kw)
                if response.status_code in good_codes:
                    return response
            return 'no good response in %s attempts' % max_tries
        return inner
    return outer


class MockResponse(object):
    codes = [100, 200, 201, 300, 400, 404, 500]
    def __init__(self, url, **kw):
        self.status_code = random.choice(self.codes)
        self.text = 'mock web service response. %s' % time.ctime()


def make_request(url):
    return MockResponse(url)


@repeat_until_status_code_in([200, 201], max_tries=7)
def yet_another(url):
    return make_request(url)


@repeat_until_status_code_in([200], max_tries=2)
def and_one_more(url):
    return make_request(url)
{% endhighlight %}

Seeing the two different versions immediately suggests a generalization to
cover both scenarios.  And that will take us to the new repo.... 

[repeat_until_satisfied](https://github.com/cary-miller/repeat/blob/master/until.py)




{% highlight python %}


{% endhighlight %}



* about this
* that
* the other

{% highlight python linenos %}
def foo():
    print 'bar'

{% endhighlight %}


--

[Discuss RDD on Hacker News](http://news.ycombinator.com/item?id=1627246)
