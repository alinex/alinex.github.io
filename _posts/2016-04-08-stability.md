---
title: Node Modules Stabilized
layout: post
tags: NodeJS Development
---

No news for some time but I was busy bringing some of my modules to production.
In this phase a lot of bugs were identified, analyzed and fixed in a lot of the
base modules. In the following parts I will explain some of them.

Report Creation
-------------------------------------
The [report](http://alinex.github.io/node-report) module is used in production
for output on the console and in mails. Multiple bugs in the console transformer
were fixed and some in markup generation. They all lead to wrong and corrupted output.

Mail module
-------------------------------------
As I saw that I need the mail functionality and specifically the setup based on
the [config](http://alinex.github.io/node-config) in multiple modules I decided to
create it's own wrapper. The [mail](http://alinex.github.io/node-mail) package
handles the configuration, sends the mail and analyze the success.

Util Package
--------------------------------------
Also in the process of centralized code used in multiple places I added new
functionality to the [util](http://alinex.github.io/node-util) package like:
string.toRegexp() and string.toList() or array.unique(). Also the object module
got an alternative method object.extendArrayReplace() which in comparison to the
normal method will replace arrays and only extends the real objects.

Validator
---------------------------------------
As I used the [validator](http://alinex.github.io/node-validator) through the
[config](http://alinex.github.io/node-config) class to get preconfigured templates
from configuration files I saw that the default helpers from handlebars are not
enough. I made same more and added an existing library of helpers to get more power
into templating.

Applications
------------------------------------
The applications for which all of this was made were the [scripter](http://alinex.github.io/node-scripter),
the [dbreport](http://alinex.github.io/node-dbreport) and [mailman](http://alinex.github.io/node-mailman).
Look into their documentation to see what they are for, but you only see the real
power of them if they are configured correctly for your needs.


_That were the main changes within the last month._
