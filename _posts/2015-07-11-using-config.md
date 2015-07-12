---
title: Using Config
layout: post
tags: Config Validator Example
---

In this article I will show you how you make your application configurable with
the power of validation. You can then use the configuration file to customize
your app for each individual person.

This article will show you how to

- install it
- create your configuration file
- create schema
- selfcheck the schema
- initialize config
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


Create Configuration File
------------------------------------------------------------------
As the next step I will first create the basic configuration file as default
or example.

If it should be the default configuration if no other given place it into
`var/src/config` as an example place it into `var/src/example`.

My file then lloks like this `myapp.yml`:

``` yaml
# Setup for my app
# =================================================
# Default settings for the spplication, you may overwrite it with the settings
# in the application's var/local/config folder or in /etc/myapp or ~/.myapp.

# Greeting message (variables are possible)
greeting: Welcome {{ name }} and have fun with this app.

# Start timeout
timeout: 1m
```

Here I used the YAML format because I like it but you may use also JSON, INI, XML...


Create Schema
------------------------------------------------------------------

Now this could be done earlier but I like to have an example file first.

So now I will define the concrete structure in a file called `configSchema.coffee`:

``` coffee
# Check definitions
# =================================================

module.exports =
  title: "MyApp configuration"
  description: "the configuration for my special app"
  type: 'object'
  allowedKeys: true
  mandatoryKeys: true
  keys:
    greeting:
      title: "Message"
      description: "the greeting message to display to the user"
      type: 'handlebar'
    timeout:
      title: "Time to Wait"
      description: "the time time wait till presenting the greeting"
      type: 'interval'
      unit: 'ms'
```

This file first sets a general title and description for the whole schema. Then
`allowedKeys` and `mandatoryKeys` specify that only the following keys are possible
and all are mandatory. The `keys` specify each setting.

The `greeting` entry is defined as handlebars so you can use the variable
`{{ name }}` within it.
The timeout is an interval which you can specify with natural settings like
1m (one Minute) or 1h 30m 30s 100ms (1 hour, 30 minutes, 30 seconds and 100 milliseconds).
This value will be converted into ms.


Selfcheck the Schema
------------------------------------------------------------------

To ensure that everything is correct we will first check for a valid schema definition
using a small mocha test.

To do so we need the validator which is used within the configuration library directly
and therefore have to install it as development dependencies. And to make easy
checks we also integrate the chai library for later use in the tests:

``` bash
npm install alinex-validator chai --save-dev
```

And we create a test case under `test/mocha/index.coffee`:

``` coffee
chai = require 'chai'
expect = chai.expect

describe "Base", ->

  Exec = require '../../src/index'

  describe "config", ->

    it "should run the selfcheck on the schema", (cb) ->
      validator = require 'alinex-validator'
      schema = require '../../src/configSchema'
      validator.selfcheck schema, cb
```

That's all, we now can test the schema each time using:

``` bash
builder -v -c test
```

The output will look something like:

    Working on ./
    run automatic tests
    Linting coffee code
    ✓ src/configSchema.coffee
      ✓ src/index.coffee

    ⚡ Warning! » 0 errors and 0 warning in 2 files
    Run mocha tests

      Base
        config
          ✓ should run the selfcheck on the schema

      1 passing (28ms)

And if something goes wrong try debugging like:

``` bash
DEBUG=* builder -v -c test
```


Initialize Config System
------------------------------------------------------------------

Before using the new configuration we have to setup the management by adding a
search uri. This will be done in an `init()` method of our application:

``` coffee
init = (cb) ->
  # set module search path
  config.register 'myApp', fspath.dirname __dirname
  # add schema for module's configuration
  config.setSchema '/exec', schema, cb
```

Because we didn't specify any uri in the register call it will load all
configuration files found in any format.

The search will be at:

- var/src/config/*
- var/local/config/*
- ~/.myApp/config/*
- /etc/myApp/*

While the last one has precedence over earlier ones.


Load the Configuration
------------------------------------------------------------------

Within a module the actual loading may be an extra step to allow the main app
to control it. But in an application you can directly do loading at the end of the
init() method:

``` coffee
init = (cb) ->
  # set module search path
  config.register 'myApp', fspath.dirname __dirname
  # add schema for module's configuration
  config.setSchema '/myapp', schema, (err) ->
    return cb err if err
    # load configuration
    config.load cb
```

After this function is run you can access the configuration data.


Use the Configuration
------------------------------------------------------------------

to use the configuration we can now implement a short main method:

``` coffee
main = (cb) ->
  init (err) ->
    return cb err if err
    conf = config.get 'myapp'
    setTimeout ->
      console.log conf.greeting 'Alex'
    , conf.timeout
```

The output after 3 seconds will be:

``` text
Welcome Alex and have fun with this app.
```

