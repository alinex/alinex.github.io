---
title: Major Release of Validator
layout: post
tags: Validator
---

About two weeks ago I finished the rewrite on the
[Validator](https://alinex.github.io/node-validator) module which was necessary
to make the references more powerful.

> It's a bit late but better as neither ;-)

The major changes are:

- made it completely asynchronous
- use powerful reference definitions
- multiple sources, filters and operations with references
- extended the validator types with: ipaddr, handlebars,

This version is not backward compatible because the calling syntax changed to only
support async calls with an option map. Also the schema definition changed slightly
for object and array types. And at last íf you already used the rudimentary references
forget everything and look at the new system.


See all the individual changes in the
[Changelog](http://alinex.github.io/node-validator/Changelog.md.html).
And how to use it in the Manual for [Validator](https://alinex.github.io/node-validator).

> But the main use will be in the [Config](https://alinex.github.io/node-config)
> system which also will be rewritten from scratch.
