---
title: CoffeeScript
layout: post
tags: CoffeeScript
---

As I started writing javascript for Node.JS I got a lot of problems caused by
missing or wrong braces. This was the time I found out about coffee script.
I see at as an easier and more readible version of javascript.

I will not give an complete tutorial or learning session here but give you an
idea of what you may do with it. Mostly I will show you the coffee code and the
corresponding javascript code.


What is CoffeeScript
------------------------------------------------------------------
Coffee script is not a new programming language but a new and optimized notation
for javascript. The coffee files can be transcoded into javascript and run directly
but you may also compile it to javascript before using it.

A lot of bad habits of javascript are fixed in CoffeeScript but the most pregnant
feature is the changed syntax. While javascript uses C-style syntax CoffeeScript
uses indentation for block building as known from Python/Ruby.

Read more about [CoffeeScript](http://coffeescript.org/) on their website.

You will also find how to install and call CoffeeScript on the above website.


Conditional Call
------------------------------------------------------------------
If the variable `x` has the value 3 a short message should be given:

``` coffee
if x is 3
  console.log 'is three'
```

``` javascript
if (x === 3) {
  console.log('is three');
}
```

First you see that the round and curly braces are missing in coffee - they are
not necessary. Also missing is the semicolon at the end of an function. Also
the comparison `is` always compiles to `===` which is better than the `==`
comparison in javascript (because the later one is not type secure).


Functions
------------------------------------------------------------------
Also very handy is the function declaration using the arrow operator.

``` coffee
fn = (x=0) -> x * 3
```

``` javascript
var fn;
fn = function(x) {
  if (x == null) {
    x = 0;
  }
  return x * 3;
};
```

Like you see it is easy to set default values for parameters if not given.


Function Stacking
------------------------------------------------------------------

As it comes to asynchronous functions I really find coffee better readable:

``` coffee
work = (cb) ->
  step1 (err, res) ->
    return cb err if err
    step2 (err, res) ->
      return cb err if err
      step3 (err, res) ->
        return cb err if err
        cb null, 'all done'
```

``` javascript
var work;
work = function(cb) {
  return step1(function(err, res) {
    if (err) {
      return cb(err);
    }
    return step2(function(err, res) {
      if (err) {
        return cb(err);
      }
      step3(function(err, res) {});
      if (err) {
        return cb(err);
      }
      return cb(null, 'all done');
    });
  });
};
```

In javascript the closing brackets are really nasty.


Transform
------------------------------------------------------------------
If you start to learn coffee you may use the [Online conversion](http://js2.coffee)
which allows you to transform in both directions so you can see the difference.

I for my part write my own code in coffee script and compile them to javascript
in the packaging process. So if you take the final package there is pure
javascript so on production you won't need the extra preprocessing step.
See the [Builder](http://alinex.github.io/node-builder) documentation on how I do this
or read the [how to create packages using builder](http://alinex.github.io/2015/06/27/builder.html)
article.


Want to know more?
------------------------------------------------------------------
Give me a hint as comment on this Article and I will extend this the way you want.
