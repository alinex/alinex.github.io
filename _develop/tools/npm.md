---
title: NPM Package Manager
layout: develop
---

Short description of how to best work with npm.

Read more on the following pages:

* TOC
{:toc}


Application Installation
-------------------------------------------------

This is done using:

	> npm install -g <package>

And it is updated using:

	> npm update -g


Development
-------------------------------------------------

While developing in node you should go into the applications root folder from
there you may add packages which are specified in package.json:

    > npm install // install new ones
    > npm update  // update already installed
    > npm dedupe  // remove duplication if possible

To only add a new package into the package.json you may instead call:

    > npm install <package> --save       // add to dependencies
    > npm install <package> --save-dev   // add to development dependencies

To publish to npm you have to call:

    > npm adduser

This will ask you about your user details (name, password, email). Afterwards
you may publish modules:

    npm publish  // called from the modules directory


Upgrade to newest package
-------------------------------------------------

``` bash
npm install -g npm-check
npm-check    # to test
npm-check -u # to update
```


Small tricks
-------------------------------------------------

### Loglevel on node v0.10

If the output of npm is too noisy for you (like for me) change it with:

    > npm config set loglevel

A less noisy level is `warn`.

### NPM Failure

This can often be caused by permission problems or wrong files in cache. Best is
to first remove the local cache and try again.

``` bash
sudo rm -rf ~/.npm
```


Package Versions
-------------------------------------------------

While developing I try to be as open as possible in the required versions. So
I hope all developer follow standards and don't change the API within a minor
version. So mostly everything till the next major version is allowed in
package.json.
