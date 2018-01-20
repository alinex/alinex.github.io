---
title: Admin Server working
layout: post
tags: NodeJS JavaScript Feathers Server REST Swagger
---

Within the last week I had time to stabilize the server part and finish it up. The final server looks like the following.

<img src="/images/Screenshot_20180120_200712.png" class="img-responsive center-block" />

# Configuration

Within the `config` directory the following configurations:

    default.json      # base configuration
    production.json   # used if run with NODE_ENV=production (`npm start`)

In this files you may change something like the `hostname`, `port` or the authentication.
More complex things should be changed in the code.

# Static, public

Within the `/public` path I have all files which will be served directly as they are:

    index.html        # the homepage
    web/              # the web client
    download/         # links to desktop app downloads
    error/            # error pages will be used on demand
      401.html
      404.html
      default.html

To integrate the web client the `web` directory is a softlink to the client's `dist` directory.

# Logs

While started using `npm` the logs will be stored automatically into the `logs` directory:

    access.log
    error.log

# Codebase

The base files are:

    index.js            # Start script used to run the server
    app.js              # Setup of the express server and the middleware
    app.hooks.js        # General hooks
    logger.js           # Setup for winston logger
    authentication.js   # Setup of authentication
    channel.js          # setup of communication chanels to the client

And then the concrete logic is split in the following directories:

    middleware          # for additional middleware
    services            # all the REST services
    hooks               # scripts to be used in hook setups
    models              # data models

## Services

Most services contain three files:

    xxx.service.js      # the service setup
    xxx.hooks.js        # linking to hook scripts
    xxx.api.js          # API documentation (used by swagger)

## Core Services

Three core services are already included:

__swagger__ includes the [Swagger](https://swagger.io/) API documentation with test possibilities

__logtail__ includes a web tail to display the servers last log lines

__users__ a real service which is used for authentication, too


_Alexander Schilling_
