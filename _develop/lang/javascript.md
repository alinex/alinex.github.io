---
title: JavaScript Tips & Tricks
layout: develop
---

Some things or tricks to know then working with JavaScript.


Events
-------------------------------------------------

The 'error' event is a special event which will throw an Error if no listener
registered.


Iterator (ES6)
-------------------------------------------------

An iterator is used to step over a list of objects. Therefore the `next()`
method can be used to retrieve the next value in the sequence. At the end a
`StopIteration` Exception is thrown. It may be used manually or in a `for each`
or `for ... in` loop.

    var data = { name: 'Alex', country: 'Germany' };
    var it = Iterator(data);
    for (var pair in it)
      print(pair); // prints each [key, value] pair in turn

See more at [MDN:Iterators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/The_Iterator_protocol).


Generators (ES6)
-------------------------------------------------

A generator is like an iterator but it won't have a fixed set to iterate over but
will generate the values on each iteration (on demand). It's a new programming
concept introduced with EcmaScript6 which will be implemented in Node 0.12 or
may be used in Node 0.11 using the `--harmony` flag.

Within a generator you may use the `yield` keyword to pause and resume.

See more at [MDN:Generators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*)
and [MDN:yield](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/yield).
