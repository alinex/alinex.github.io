---
title: Styleguide
layout: develop
---

This guide should give an overview of the general style within the alinex system
and it's packages. It is neither meant as a hard limit but neither as some
nice to have rules. So as much as possible this rules have to be followed.


General layout
-------------------------------------------------
Within the code I use 2 spaces for indention neither tabs because they make
reading problematic and also are not suited for coffee script if mixed with
spaces.


Variables
-------------------------------------------------
Over all modules some common variable names will be used for the same values:

- `cb` - for the callback method
- `done` - alternatively used for the callback for better reading
- `err` - for an error message object
- `ex` - mostly the exception in a `try...catch` block

Classes start with an Uppercase letter:

``` coffee
test = new Test
```

To mark private properties/functions they may start with an underscore.

Modules are always imported into a variable which is named after the module
and if the module exports a class the uppercase name is used.


Asynchronous code
-------------------------------------------------
Through the whole code as much as possible only asynchronous code should be used
without blocking. That brings the most performance out.

### Callbacks

These code follows the node.js convention of providing a single callback as
the last argument of your asynchronous function.

To not make it too complex the async function may call it's callback synchronously
in the same eventloop or later. It is no true asynchronity by definition, so
if you need it maybe think about your code structure or call the function
through `process.nextTick()` yourself.

### Async module

You may also use the [Async](https://github.com/alinex/node-async/) module. It
brings you a lot of methods to make asynchronous calls parallel or serial.

### Events

Often events are also used to make use of the asynchronous behavior in class
objects.


Error/Exception handling
-------------------------------------------------
Error and exception handling will be done in JavaScript/CoffeeScript in the
following ways:

- Synchronous code will return an Error object instead of the normal return
  value:

``` coffee
    myfuncSync = () ->
      x = doSomething()
      if x is 1
        return new Error "Failed calculation"
      return x

    result = myfuncSync()
    if result instanceof Error
      console.error result.message
```

- Asynchronouse code should send the error as first parameter to the callback
  method or `null` if no error occurred:

``` coffee
    myfunc = (cb) ->
      x = doSomething()
      if x is 1
        cb new Error "Failed calculation"
      else
        cb null, x

    myfunc (err, result) ->
      if err
        console.error err.message
```

- And at last an error may be thrown only if it is a hard error which signals
  an fatal error which may stop the overall process.

  Such an error may be catched in a try block, in a domain or on the process.

- Another solution is to use eventful methods which emit an `error` event

Read more in the [errorHandler](https://github.com/alinex/node-error/)
documentation.


Control flow
-------------------------------------------------
To make the code more readable and prevent some hanging else-statements which
you have to search to which indention level it belongs to return or callback
as fast as possible.

Bad:

``` coffee
if err
  doSomething (err) ->
    return cb err
else
  return true
```

Good:

``` coffee
return true unless err
doSomething (err) ->
  return cb err
```


Documentation
-------------------------------------------------
All the code in any language will be documented inline using comments as
possible in the specific language. No JavaDoc or alike have to be used.
Only plain markup which will be automatically detected and converted to
documentation.

In each exported method the parameters will be documented in detail and the
callback methods with their values, they will get.

Some overall documentation like this will be stored in special markup files
ending with `.md`.


Debugging
-------------------------------------------------
Best use the node-inspector for this:

``` bash
sudo npm install -g node-inspector
node-inspector
node --debug-brk lib/cli.js -v
```


Testing
-------------------------------------------------
Linting is used to precheck the code. This will not only check the syntax but also
the style and the above conventions of the styleguide.

Mocha unit tests are used to check individual parts and the overall
functionality. As much as possible should be tested but not only single units
but all interface calls. An test coverage of 100% should be the goal.


Publishing
-------------------------------------------------
To publish new packages the following steps should be done:

1. Check dependencies and their version in package.json (maybe run `npm outdated`)
2. Cleanup to remove test packages
3. Install and update packages
4. Run the test suite
5. Push code to repository
6. Publish new package
7. Create and publish new documentation

The tasks are done in an easy way using the
[alinex-builder](http://alinex.github.io/node-builder).

``` bash
# step 1-3
builder -c clean --auto -c update
# step 4-7
builder -c test -c publish --minor -c doc --publish
```

Configuration
-------------------------------------------------
The general configuration is stored in files to be also available without
database connection. To make it easy readable and maintainable it should
be written in yml rather than json.

[alinex-config](http://alinex.github.io/node-config/) helps in working with
such files.


Dependencies
-------------------------------------------------
To use singleton modules the dependencies for specific versions should be as
open as possible. This makes it possible to use:

``` bash
npm dedupe
```

This will flatten down the modules to the uppermost common module in hierarchy.

Peer dependencies are also possible, in which a sub module specifies which
parent it needs. This will be specified in the `peerDependencies` section.
