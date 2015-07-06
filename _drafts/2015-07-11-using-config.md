---
title: Using Config
layout: post
tags: Config, Application
---

In this article I will show you how you make your application configurable with
the power of validation. You can then use the configuration file to customize
your app for each individual person.

This article will show you how to

- install it
- create your configuration file
- create schema
- selfcheck the schema
- load the configuration
- use the configuration

First you have to create your application structure. See the
[Builder](/2015/06/27/builder.html) description of how to make your application's
skeleton.

Add Configuration
------------------------------------------------------------------

We will use the [Config](https://alinex.github.io/node-config) module to reach
our goal. So the first step is to add it to your application:

``` bash
npm install alinex-config --save
```

After this step the config system is installed and added to your package.json.


