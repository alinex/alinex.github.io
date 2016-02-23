---
title: CoffeeScript
layout: develop
---

CoffeeScript is an easier syntax for JavaScript. It has a syntax inspired from Python
and Ruby. The code will be transformed into real JavaScript before executing. This
can be done on the fly or as a compiler before packaging and executing it in the
productive environment.


Why To Use It
-------------------------------------------------

CoffeeScript is used as development language because it is very easy to write
and read. In my opinion it makes development and maintenance easier and faster.
Specially in the callback sequences of JavaScript.

This page lists some tricks and tips which are mostly not mentioned in the
official docs.


Strings
-------------------------------------------------

### Check for substring

``` coffee
if ~message.indexOf 'test'
```

The above syntax uses the tilde as bitwise or operator to get a boolean
readable value. If the substring is found it will be true (any number), and
false (0) if it isn’t. or use the following to get a real boolean type:

``` coffee
x = Boolean ~message.indexOf 'test'
```

Or use the negation:

``` coffee
if !~message.indexOf 'test'
```


Objects
-------------------------------------------------

### Check for empty object

``` coffee
unless obj? and Object.keys(obj).length
```

This will run the following code only if the object under test is not defined
or is an empty object.


Control flow
-------------------------------------------------

### Try without catch

``` coffee
try
  funcWhichMayThrowError()
```

If you ommit the catch the error will be supressed.

``` coffee
try {
  funcWhichMayThrowError();
} catch (_error) {}
```


For loops
-------------------------------------------------

Loop over array:

``` coffee
for element in arr
```

Counting loop:

``` coffee
for i in [0..n] by 1
```

Reverse loop:

``` coffee
for i in arr by -1
```

Loop over object:

``` coffee
for key of object
  ...
for key, value of object
  ...
```


Callbacks
-------------------------------------------------

To prevent checking for a given callback method on every call you may give it
an empty default function on parameter definition:

``` coffee
test = (src, cb = -> ) ->
  console.log 'do something'
  cb()
```


Classes
-------------------------------------------------

Classes are made really easy using CoffeeScript:

``` coffee
# define a class
class Test
  # make a constructor method
  constructor: ->

# create instance
t = new Test
```

Use the `@` sign in parameters to store the value in the same instance property:

``` coffee
class Test
  # store given name in this.name
  constructor: (@name) ->

# add another prototype to class
Test::done = true
```

Inheritance is also made easy:

``` coffee
class Test
  constructor: (@name) ->

# extend the class
class Test2 extends Test
  constructor: ->
    # call the parent constructor
    super 'numberTwo'
```

Local variables are created using `=` but properties are defined using `:`:

``` coffee
class Test
  # local class variable/function
  foo = 1
  # instance variable/function
  bar: 2
  # or from the constructor
  constructor: ->
    @baz = 3
```

You may also use class properties/funtions

``` coffee
class Test
  # static class variable/function
  @foo: 1
  @bar: (name) ->
  constructor: ->
    # access statics
    Test.bar()
    # or
    @constructor.bar()

# access from outside
Test.foo
Test.bar 'baz'
test = new Test
test.constructor.foo
```
