---
title: Current Development
layout: post
tags: Development, Database, Server
---

Over the summer the planning and coding of more and more alinex modules were
going on and on but in a slower peace. Today, I will show you what changed and what
is going on the next days.

### Server

The [Server](http://alinex.github.io/node-server) concept was finished in it's basics
giving a stable highly configurable server using the [Config](http://alinex.github.io/node-config)
module.

Just now it supports multiple port binding, virtual hosts, and context based
applications. Through the space definition a base for application specific configuration
is given.

A full debugging using DEBUG=... environment settings and he overload protection
is also build in and can be customized using configuration.

From a functional view plugins are supported to add functionality in an easy way.
Contained are the configurable logging support and a static file provider.

That's only a start but it shows that from there on I may easily add everything
which is needed in the future.

### Config

Within the [Config](http://alinex.github.io/node-config) module I had to make some
smaller fixes to make it work as planned.

### Validator

Just recently I added a datetime validation to the
[Validator](http://alinex.github.io/node-validator) which is also used within the
[Config](http://alinex.github.io/node-config). The datetime type allows you to
specify a time or date and also a range in standardized or human readable formats.

### Database

And just now I made a concept bringing my [Mysql](http://alinex.github.io/node-mysql)
wrapper module one step further to a general class like the others. Under the name
[Database](http://alinex.github.io/node-database) I will create a module which can
work with multiple databases like:

- mysql
- postgresql
- sqlite
- mongoDB
- elasticsearch

All through the same general approach giving the developer the same API independent
of the used data store. SQL and other dialects are possible direct, as JSON and with
parameters. And also supporting access through ssh-tunneling.

As a first step only the mysql database driver is added but the others will follow
later.

Come again in some days to be kept on track.