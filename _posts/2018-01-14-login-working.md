---
title: State of Admin Portal (Milestone 1)
layout: post
tags: NodeJS JavaScript Server Client Application Admin Portal
---

This should be a summary of what I got and how it is made as I reached my first big milestone.

# Basics

The first roundtrip, as a summary of my last posts, was to make a universal client application with a REST server to get it's data. It should be possible to authenticate and be build in a modular and scalable way.

I did this in my two repositories:
- [Admin Client](https://github.com/alinex/node-admin)
- [Admin Server](https://github.com/alinex/quasar-admin)

This first big milestone was reached by me now.

## Architecture

The application consists of two components:

1. The **Frontend Client** which is used as the interface for the user on any device.
2. **REST Server** which holds the data for the frontend display.

The Frontend itself may be hosted on the same webserver as the REST Server or on
any other static server. It may also be used ass desktop or mobile-app.

# REST Server

First the server providing the complete data.

__Features__

- stateless using simple Java Web Token
- websocket (Realtime API) or HTTP REST
- service oriented architecture
- NodeJS 8
- server validation
- multiple database support
- logging events

__Planned__

- authentication logging
- attruíbute based authorization
- multi core support

## Technologies

- [ExpressJS](http://expressjs.com/de/) as webserver
- [Feathers](https://feathersjs.com/) REST and realtime API
  - [Authentication](https://docs.feathersjs.com/api/authentication/server.html)
  - [JWT](https://jwt.io/) JSON Web Token for authentication


# Client

__Features__

- universal app for browser, Android, IOS, Windows, Mac OS and Linux
- responsive design using FlexBox
- modern interactive layout with animations, shadow-DOM and data binding
- JavaScript ES8, Stylus CSS
- client validation
- component based widgets

__Planned__

- upgrade to upcomming quasar v0.15
- better design
- attribute based authorization
- with test area
  - public test page
  - private test

## Technologies

- [Vue.js](https://vuejs.org/v2/guide/installation.html) as the base technology for the client interface
- [vue-router](https://router.vuejs.org/en/) for client side routing
- [Vuelidate](https://monterail.github.io/vuelidate/#getting-started) for form validation
- [Vuex](https://vuex.vuejs.org/en/) centralized state management
- [feathers-vuex](https://github.com/feathers-plus/feathers-vuex) feathers server integration
- [JWT](https://jwt.io/#debugger) JSON Web Token for authentication
- [Quasar Framework](http://quasar-framework.org/guide/) components and base structure with electron and cordova integration
- [Stylus](http://stylus-lang.com/) CSS language


# Application

This describes the overall functionality:

__Features__

- authentication
- test area (only while developing)

__Planned__

- final layout
- user administration module
- chat application module


# Further steps

The development will slow down a bit but the next milestone will include the above features described under planned. It will also use a mongo db instance for the first modules.

_Alexander Schilling_
