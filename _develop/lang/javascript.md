---
title: JavaScript
layout: develop
---

JavaScript is a scripting language which grows out of the Netscape Browser. It
is now over 20 years old and since it started as a browser language in one browser
it grew to the ultimate web scripting language supported in all browsers. In the
last years the Node.JS project brought JavaScript to a general language usable
on the server or desktop.
The core is standardized as ECMAScript in different Versions. The language itself
was kept the same for some years but just now it develops further and get more
modern in ECMAScript6 or ECMAScript7.

Find more about JavaScript on the server under [Node.Js](nodejs.html).


Specification
-------------------------------------------------
JavaScript is an interpreter language with a C-like syntax. It is a dynamic typed
language in which variables point to values which are associated to types.
It is object driven in which most things are objects which are associative arrays
with prototypes. Prototypes are used for inheritance instead of classes. But class
based features could be simulated through prototypes, too.
The language is event driven and it's core is an event engine through which the
functions will be called. This gives the possibility of doing things in parallel
within one process while waiting for external data.


Tips and Tricks
-------------------------------------------------

Some things or tricks to know then working with JavaScript.


### Events

The 'error' event is a special event which will throw an Error if no listener
registered.

### Iterator (ES6)

An iterator is used to step over a list of objects. Therefore the `next()`
method can be used to retrieve the next value in the sequence. At the end a
`StopIteration` Exception is thrown. It may be used manually or in a `for each`
or `for ... in` loop.

    var data = { name: 'Alex', country: 'Germany' };
    var it = Iterator(data);
    for (var pair in it)
      print(pair); // prints each [key, value] pair in turn

See more at [MDN:Iterators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/The_Iterator_protocol).

### Generators (ES6)

A generator is like an iterator but it won't have a fixed set to iterate over but
will generate the values on each iteration (on demand). It's a new programming
concept introduced with EcmaScript6 which will be implemented in Node 0.12 or
may be used in Node 0.11 using the `--harmony` flag.

Within a generator you may use the `yield` keyword to pause and resume.

See more at [MDN:Generators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*)
and [MDN:yield](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/yield).
