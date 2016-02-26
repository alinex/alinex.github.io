---
title: Handlebars Templates
layout: post
tags: Handlebars
---

Since some months I have support for handlebars as specific type included into
[validator](http://alinex.github.io/node-validator). But I was now using it
more I got some problems.

First the official website and it's description of the syntax is a bit to
unstructured and somehow not complete. The other thing is I can't use it how
I need it without some more helpers.


Syntax Documentation
===================================
For the first thing I started to make my own [handlebars reference](/develop/lang/handlebars.html)
which is a compact reference for all the possibilities with some small examples.
I will extend it as my knowledge extends on demand.


Enlarge Handlebars Support
====================================
To optimize for the use in different tools I had to rewrite the
[validator](http://alinex.github.io/node-validator) type handler to also support
some of my own helpers.

To start with I added:

- dateFormat
- dateAdd

They may be used to format the date also in local format and maybe manipulate it
before.
