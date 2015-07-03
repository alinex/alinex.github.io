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

Details of changes
------------------------------------------------------------------

I only describe the major changes in it's core. See the links below for more information.

### Asynchronous calls

The main method will validate and sanitize the value or value structure:

``` coffee
validator.check
  name: 'test'        # name to be displayed in errors (optional)
  value: input        # value to check
  schema: schema      # definition of checks
  context: null       # additional data (optional)
, (err, result) ->
  # do something
```

Also the `describe` and `selfcheck` methods work with an similar options object.

### References

References point to values which are used on their place. You can use references
within the structure data which is checked and also within the check conditions.
Not everything is possible, but a lot - see below.

The syntax looks easy but has a lot of variations and possibilities.

``` text
<<<source://path>>>
<<<source://path | source://path | default>>>
<<<source://path#{type:"integer"} | source://path | default>>>
```

Within the curly braces the source from which to retrieve the value is given.
The source is given in form of an URI.
Like you see in line two you may use multiple fallback URIs and also a default
value at last.
And at last in the third line you see how to add a special check condition
after an URI. If this fails the next URI is checked.

The path may also have different possibilities based on the `source` protocol
type.

### New Types

__ipaddr:__

The value has to be an IP address. The addresses may be converted from IPv6 to
IPv4 and from IPv4 to IPv6 if possible. And you may allow or deny some ranges.

``` coffee
validator.check
  name: 'test'        # name to be displayed in errors (optional)
  value: '192.168.12.20' # value to check
  schema:             # definition of checks
    type: 'handlebars'
    deny: ['private']
    allow: ['192.168.12.1/24']
, (err, result) ->
  # this will validate without error
```

__hanlebars:__

This easy type will check the text which may contain [handlebars](http://handlebarsjs.com/)
syntax and make a function out of it. This contains the compiled handlebars template
and can be called with the context to use:

``` coffee
validator.check
  name: 'test'        # name to be displayed in errors (optional)
  value: 'Hello {{name}}!' # value to check
  schema:             # definition of checks
    type: 'handlebars'
, (err, result) ->

  # then use it
  console.log value
    name: 'alex'
  # this will output 'Hello alex!'
```

More Information
------------------------------------------------------------------

See all the individual changes in the
[Changelog](http://alinex.github.io/node-validator/Changelog.md.html).
And how to use it in the Manual for [Validator](https://alinex.github.io/node-validator).

> But the main use will be in the [Config](https://alinex.github.io/node-config)
> system which also will be rewritten from scratch.
