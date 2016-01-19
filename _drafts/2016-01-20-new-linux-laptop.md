---
title: Install new Linux Laptop
layout: post
tags: Linux
---

Time is going on and nearly everything in the IT will get more bloated over the Time
but my notebook never grows. So just now I was developing on a machine on which I
had to close the browser and editor so that I can run some unit tests.

My old notebook is a Samsung R505-Aura from 2008 with an AMD Athlon 64 X2 and
2GB RAM. Now I got an Acer Aspire E5 with i7 and 8GB RAM.


First Impression
================================================================================
First the notebook itself looks good but the plastic case is not made perfectly
designed but the overall fell of the machine, keyboard and touchpad is good.


Installation
================================================================================

The first problem I got was booting from the USB Stick or CD. I had to enable
the bootmenu (Bios with F2 on Boot -> set F12 Bootmenu to enabled). After that
I could boot an UEFI compatible Linux but got problems with the touchpad. To fix
this I had to set it to 'Standard Mode' (default was 'Advanced') in the BIOS.

My next problem was the booting. After successfully installing the laptop always
boots into Windows and don't ask for Linux. I didn't matter how I configured it.
To fix this I also switched from UEFI to legacy BIOS and moved my harddisk in the
boot order higher as the WindowsBoot entry.

That got me a workable system but the WLAN chipset won't run with Ubuntu 15.10.
Before taking to much time there I used an USB WLAN Stick. I will check for this
on the next release of Ubuntu 16.04 LTS.


Fazit
================================================================================
The end result is fine. I got a system working fast and doing everything I want
for a reasonable price.
