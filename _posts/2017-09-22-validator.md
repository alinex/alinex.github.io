---
title: New Validator Module
layout: post
tags: JavaScript config validator
---

The last months I was hard working on a rewrite of the [validator](https://github.com/alinex/node-validator).
It is the first module in a complete new generation of scripts.

Sorry that I had no posts online the last weeks but I was heavy at work.

# Environment

My idea was to switch from my CoffeeScript to ES6 and newer technologies. I had to read and check out
what I need and how to do it best. It was no easy going and for everybody to do the same I put
everything together in a book about [https://alinex.gitbooks.io/nodejs/](NodeJS Module development).

While there were efforts bringing CoffeeScript to a more modern version I had no time to wait and decide.
So I switched to direct writing JavaScript but with the newest additions like ES6, and also up to
ECMAScript2017. To run it while not everywhere supported transpilation with polyfills is used.

Till now CoffeeScript V2 is released but I will keep going with the ES.Next approach. Because I also
love the very good optimizing and type safety added using ESLint and Flow in test and directly in the
editor.

As I also did previously it is nearly complete covered by functional tests.

# Asynchronity

To make references and inclusion of external data (added in v2) easier I made it completely asynchronous
from the ground up. This is mainly based on `Promise` so that it can also be easily used with `async`
and `await` for you.

Not only the validation but also loading of rarely used modules is added in asynchronous fashion.

# Functionality

As V2 was based on schemas defined as objects it is now class based. This has the advantage of an
easier building of schemas which will be checked as they are defined.

Basically the functionality is kept. But as I converted one type after the other I often had further
ideas to make the same options easier to use and enhance them further.

As a result it is not backward compatible. To switch you have to implement it completely new from
the schema up.

# Configuration

I had also the idea of using this in the alinex-config module. Because the config module has only
some minor additions to the validator this functionality was brought directly into the validator, too.

It can also be used to search, combine, validate and transform configuration files into a JSON data
structure by CLI call. This can later be imported from any program without further checking.

You don't need the alinex-config module any longer.

# Checkout

If you want to now more details what the new validator can do for you have a look at [validator](https://github.com/alinex/node-validator).

_Alexander Schilling_
