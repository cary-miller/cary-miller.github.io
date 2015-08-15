Joel's Law `ALL non-trivial abstractions are leaky`
===================================================

In other words we have to understand the underlying technology beneath our target
system.


Examples

nfs / cifs

> mv /mnt/scr01/blah /mnt/scr02/blah # fails
  mv /mnt/scr01/blah /mnt/scr02/blah # used to work


function making web service call
    fails due to
        timeout
        network prob


redis - webdis - webdis.py
es - whatitsname - whatsit.py
rabbitmq -
zeromq -

nfs / cifs, redis, es, rabbitmq, tickettool
    all abstract away the notion of separate computers.
        for specific task

# principles #
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

tickettool

ins-queue
    r2.py


promises - async - fetch result that takes arbitrary time


good local abstractions
    webdis.py
    es.py
    repeat_until_satisfied


bad/leaky local abstractions
    nfs/cifs  re file moving
    no.   The question re an abstraction is not so much "Is it good or bad?"
    but more,  "What are its limits?".





