---
title: Webserver Benchmarking
layout: post
tags: development go vs rust
---

Compare Rust with Go (Performance)
=====================================================

As I want to work on a web project which needs a stable and fast web server
I made an application serving a static html file in both languages. I did not
program everything on my own but used the most popular and stable modules for
both of them.

As a result I compare them against a plain Apache 2.4 installation. To make
it comparable all serve the same very simple html file which they will found in
their base directory.

I did run all three directly after each other on the same machine (i7 4CPU Cores,
8GB RAM).

__Apache 2.4__

    $ wrk -t4 -c400 -d30s http://127.0.0.1
    Running 30s test @ http://127.0.0.1
      4 threads and 400 connections
      Thread Stats   Avg      Stdev     Max   +/- Stdev
        Latency     3.14ms   10.29ms 346.49ms   98.67%
        Req/Sec     3.51k     2.97k   13.96k    63.27%
      363271 requests in 30.04s, 115.78MB read
    Requests/sec:  12094.09
    Transfer/sec:      3.85MB

    load average: 8,36, 4,16, 2,35

__Go using net/http__

    $ wrk -t4 -c400 -d30s http://127.0.0.1:8080
    Running 30s test @ http://127.0.0.1:8080
      4 threads and 400 connections
      Thread Stats   Avg      Stdev     Max   +/- Stdev
        Latency    24.62ms   42.73ms 634.52ms   89.12%
        Req/Sec    12.86k     3.38k   25.59k    75.25%
      1537844 requests in 30.09s, 393.03MB read
      Non-2xx or 3xx responses: 467
    Requests/sec:  51104.56
    Transfer/sec:     13.06MB

    load average: 4,69, 3,83, 2,37

__Rust using Iron__

    $ wrk -t4 -c400 -d30s http://127.0.0.1:8080

    Running 30s test @ http://127.0.0.1:8080
      4 threads and 400 connections
      Thread Stats   Avg      Stdev     Max   +/- Stdev
        Latency   406.52us  463.76us  72.85ms   95.36%
        Req/Sec    39.20k    36.83k   78.90k    55.17%
      2340369 requests in 30.06s, 412.91MB read
    Requests/sec:  77864.45
    Transfer/sec:     13.74MB

    load average: 14,28, 6,16, 3,25


Resume
--------------------------------------------------------------
Apache did the least number of requests, Go was about 4 times faster but failed
for some requests. The most requests were answered by Rust with no errors. Also
the latency was very low but the system on full load.

So if performance matters Rust is the best to go but if only the pure static
delivery is needed Nginx & Co should be checked against an own implementation.

_Alexander Schilling_
