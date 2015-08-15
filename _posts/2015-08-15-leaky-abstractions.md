Joel's Law 
===================================================
`All non-trivial abstractions are leaky`

In other words we have to understand the technology underlying the target
system.


### Example 1 (`nfs / cifs`)

{% highlight bash %}
mv /mnt/scr1/blah /mnt/scr2/blah # fails.  worked before
{% endhighlight %}

Why does it fail where it formerly worked?   Something changed in the way the
systems were mounted.




### Example 2 (`web service client`)

fails intermittently due to

* timeout
* network prob


nfs / cifs, redis, es, rabbitmq, logtool

* redis - webdis - webdis.py
* es - whatitsname - whatsit.py
* rabbitmq -
* zeromq -


nfs / cifs, redis, es, rabbitmq, logtool

        all abstract away the notion of separate computers.
            for specific task

## principles #

    abstract away the right parts (http, url-construction, retry)
        be frictionless
    do not get between the user and the service
        ie. do NOT
            be "helpful"
            devise "better" names
    generality vs specificity/speed


zap / spark

    read whole thing vs
    extract small parts


promises - async - fetch result that takes arbitrary time


good local abstractions

    webdis.py
    es.py
    repeat_until_satisfied


bad/leaky local abstractions

    nfs/cifs  re file moving
    no.   The question re an abstraction is not so much "Is it good or bad?"
    but more,  "What are its limits?".




