---
title: Development of Exec Library
layout: post
tags: Exec
---

In my effort to make all my classes more robust and powerful I looked at the spawn
module which is great but can have lots of improvements. My ideas are to allow
remote execution, better reporting, more stability and another system to not
exceed the server load.

To reach this goals I decided to take the basic ideas and make a more opened for
extensions module under the name [Exec](http://alinex.github.io/node-exec).


Old Spawn Module
------------------------------------------------------------------
This module is deprecated now and will not be developed further on. You may use
it as it is but better take the time and upgrade to [Exec](http://alinex.github.io/node-exec).

Just now as the new module reached the beta state and has reached all the functionality
from spawn I will no longer link or support the spawn module.


Current State
------------------------------------------------------------------
The library has now just the basics but stable and running. You may define
what and how to execute it in an object. What you didn't specify will
automatically set to the most used setting.

You can call tasks also asynchronously in parallel as much as you want without
an server overload. To tweak this you may define and specify the priorities
to your needs in the configuration like all values.

If something goes wrong you get a good explanation if specified the correct
checks.


Overload Protection
------------------------------------------------------------------
The new overload protection checks the following things

- ulimit exceeded - try again
- too high cpu usage - queue
- load average too high - queue
- too much processes started - queue

If processes can't be run yet and got into the queue they will be processed if
resources are available again by priority level.


Debugging
------------------------------------------------------------------
Like all my modules I added the `debug` module everywhere so you can debug also
on the live system in an easy way by setting an environment variable.

Call it using:

``` bash
DEBUG=exec* <app>
```

You may also specify more specifically what to debug.


Further Planning
------------------------------------------------------------------
The next big parts will be:

- remote execution
- interactive control
- detached execution
- piped executions

Maybe in two to three weeks I will reach this goal.
