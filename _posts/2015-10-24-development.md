---
title: Current Development
layout: post
tags: Development Database Monitoring Validator Config
---

Two weeks are gone and I made some improvements on existing modules, made the
database module stable (for mysql only) and started to finish my monitoring
application which was planned over the last 12 months.

Monitoring
----------------------------------------------------------------
Starting with the newest development first, I began to finish the
[monitor](http://alinex.github.io/node-monitor/) application. Over the last 12 months
I planned it, made some tests on the possible sensors but found out that some basic
functionality is missing.

This basic functionality was now build and brought to a stable state:

- [config](http://alinex.github.io/node-config/) - reading the complex setup from files
- [validator](http://alinex.github.io/node-validator/) - make the use easy by using
  validation and sanitation
- [exec](http://alinex.github.io/node-exec/) - executing external commands also
  over ssh (remote sensors)
- [database](http://alinex.github.io/node-database/) - to check database settings
  and to store the results

So there are no bigger problems to bring the application further on. In the first
phase the monitoring application will be fully configurable and able to be started
through the CLI interface or as a daemon. It should run some basic sensors and collect
the results and reports. Emails will be generated and the data will be stored in
a database from which you may make your reports over time with your default
database visualization tool.

Later on there may be more sensors, some automatic actors and maybe a web interface.


Package Improvements
----------------------------------------------------------------

In the last days I made the following improvements on some existing modules:

### Config

Now it is possible to set a `filter: <subdir-name>` in register call. This makes
it possible to store configuration files in different folders. So you may load
all from the default `config` folder and only some of the additional folder by
making two registration calls:

``` coffee
config.register 'app', fspath.dirname __dirname
config.register 'app', fspath.dirname(__dirname),
  uri: "#{pattern}*"
  folder: 'extras'
  path: 'app/extras'
```

This code shows how to first load all config from config folder, then the matching
ones from the extra folder. See more at the [config](http://alinex.github.io/node-config/)
description.

### Validator

After fixing a small bug it is now possible to reference values from the schema.
So you can have a schema checking that the value at one point is defined in another
position of the value structure:

Schema:

``` text
templates:
  type: 'object'
  entries: [
    type: 'handlebars'
  ]
default:
  type: 'string'
  list: '<<<context:///templates>>>'
```

Value:

``` text
templates:
  first: "Wellcome {{name}}"
  ongoing: "Hello {{name}}"
default: 'ongoing'
```


Database
----------------------------------------------------------------

After adding the SSH tunneling ability, now the database has also a working
implementation of the object notation. This allows to write the query not directly
as SQL but as an object. Before transferring it to the database it will be converted
to a standard conform SQL.

``` coffee
  conn.query
    select: '*'
    from: '@person'
    where:
      age: 30
      name: 'Alf'
  # SQL: SELECT * FROM `person` WHERE `age` = 30 AND `name` = 'Alf'
```

The next steps here will be the addition of postgresql support.




Best Regards

//Alex//