---
title: Linux System Analysis
layout: post
tags: Linux System Monitoring
---

As I worked on the new [monitor](http://alinex.github.io/node-monitor/) application
I learned a lot more over linux systems as I thought.

CPU and Memory Monitoring
----------------------------------------------------------------
As I checked for cpu, memory, network and disk stats I had to dive into the `/proc` device
device and found a lot of goodies. I learned that I often don't need to parse
the `top` output but only read one of the files and have all i need easy to parse
in my code.

So I ended up on doing lots of stuff directly like cpu frequency and number of cores:

``` bash
cat /proc/cpuinfo | egrep '(processor|cpu MHz)'
```

``` text
processor : 0
cpu MHz   : 1000.000
processor : 1
cpu MHz   : 1000.000
```
CPU usage:

``` bash
grep cpu /proc/stat
```

``` text
# -  user   nice   system idle  wait hwint swint
cpu  528498 1210070 143925 681293 122405 5 3778 0 0 0
cpu0 269496 586448 72771 656833 100104 3 1820 0 0 0
cpu1 259002 623622 71154 24459 22300 2 1958 0 0 0
```

Load average:

``` bash
cat /proc/loadavg
```

``` text
# 5m 10m  15m
0.08 0.93 1.72 1/457 18206
```

And to get all information about the memory:

``` bash
cat /proc/meminfo
```

``` text
MemTotal:        1803540 kB
MemFree:          197972 kB
Buffers:          136492 kB
Cached:           337272 kB
SwapCached:        12296 kB
Active:           587844 kB
Inactive:         603900 kB
Active(anon):     353912 kB
Inactive(anon):   395988 kB
Active(file):     233932 kB
Inactive(file):   207912 kB
Unevictable:          96 kB
Mlocked:              96 kB
HighTotal:        920392 kB
HighFree:          61864 kB
LowTotal:         883148 kB
LowFree:          136108 kB
SwapTotal:       1831932 kB
SwapFree:        1710496 kB
Dirty:                92 kB
Writeback:             0 kB
AnonPages:        708184 kB
Mapped:           101388 kB
Shmem:             31920 kB
Slab:             298260 kB
SReclaimable:     276508 kB
SUnreclaim:        21752 kB
KernelStack:        3640 kB
PageTables:        12212 kB
NFS_Unstable:          0 kB
Bounce:                0 kB
WritebackTmp:          0 kB
CommitLimit:     2733700 kB
Committed_AS:    5195368 kB
VmallocTotal:     122880 kB
VmallocUsed:       16260 kB
VmallocChunk:      56684 kB
HardwareCorrupted:     0 kB
AnonHugePages:     88064 kB
HugePages_Total:       0
HugePages_Free:        0
HugePages_Rsvd:        0
HugePages_Surp:        0
Hugepagesize:       2048 kB
DirectMap4k:       30712 kB
DirectMap2M:      882688 kB
```

Disk Monitoring
----------------------------------------------------------------

``` bash
cat /proc/diskstats
```
``` text
   1       0 ram0 0 0 0 0 0 0 0 0 0 0 0
   1       1 ram1 0 0 0 0 0 0 0 0 0 0 0
   1       2 ram2 0 0 0 0 0 0 0 0 0 0 0
   1       3 ram3 0 0 0 0 0 0 0 0 0 0 0
   1       4 ram4 0 0 0 0 0 0 0 0 0 0 0
   1       5 ram5 0 0 0 0 0 0 0 0 0 0 0
   1       6 ram6 0 0 0 0 0 0 0 0 0 0 0
   1       7 ram7 0 0 0 0 0 0 0 0 0 0 0
   1       8 ram8 0 0 0 0 0 0 0 0 0 0 0
   1       9 ram9 0 0 0 0 0 0 0 0 0 0 0
   1      10 ram10 0 0 0 0 0 0 0 0 0 0 0
   1      11 ram11 0 0 0 0 0 0 0 0 0 0 0
   1      12 ram12 0 0 0 0 0 0 0 0 0 0 0
   1      13 ram13 0 0 0 0 0 0 0 0 0 0 0
   1      14 ram14 0 0 0 0 0 0 0 0 0 0 0
   1      15 ram15 0 0 0 0 0 0 0 0 0 0 0
   7       0 loop0 0 0 0 0 0 0 0 0 0 0 0
   7       1 loop1 0 0 0 0 0 0 0 0 0 0 0
   7       2 loop2 0 0 0 0 0 0 0 0 0 0 0
   7       3 loop3 0 0 0 0 0 0 0 0 0 0 0
   7       4 loop4 0 0 0 0 0 0 0 0 0 0 0
   7       5 loop5 0 0 0 0 0 0 0 0 0 0 0
   7       6 loop6 0 0 0 0 0 0 0 0 0 0 0
   7       7 loop7 0 0 0 0 0 0 0 0 0 0 0
#  -       - device read  -   sector    time    write   -    sector  time
   8       0 sda 590222 41767 8943336 9604416 98663 200412 5142048 19478944 0 2344660 29082928
   8       1 sda1 589085 37014 8896194 9578980 96107 170459 4886952 19415820 0 2321700 28994380
   8       2 sda2 3 0 6 52 0 0 0 0 0 52 52
   8       5 sda5 951 4750 45648 24500 1933 29953 255096 42028 0 28996 66524
  11       0 sr0 0 0 0 0 0 0 0 0 0 0 0
```

And the `df` utility is used to show free disk space.


Goal
-------------------------------------------------
I will try to release a first stable version of the [monitor](http://alinex.github.io/node-monitor)
with all this in December 2015. This includes:

- a working cli syntax
- the interactive console
- possibility to run onetime analyzation
- database storage support
- daemon mode running controller on schedule

The next version coming early in 2016 will have:

- fully working explorers
- alerting with mail actor
- tested in productive environment

After that a lot of bugfixes, smaller improvements and more sensors, actors and
explorers will follow regularly.
