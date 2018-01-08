---
title: Rest Server
layout: post
tags: NodeJS JavaScript Express Feathers REST Server
---

For the new client application I need a REST server with authentication. This should be done using NodeJs, too. So I had to look for the right technologies and decided to use:

- [ExpressJS](http://expressjs.com/de/) as webserver
- [Feathers](https://feathersjs.com/) REST and realtime API
  - [Authentication](https://docs.feathersjs.com/api/authentication/server.html)

# Initial Server

The initial server is build with feathers and express supporting HTTP and socket.io
connections. But it's homepage is simple and only points to the Frontend Panel (link
should be set if released).

It supports the following methods per REST service (here the message service, cretaed later):

| Service | HTTP method | Path        |
| ------- | ----------- | ----------- |
| .find() | GET  	      | /messages   |
| .get() 	| GET 	      | /messages/1 |
| .create() 	| POST 	  | /messages   |
| .update() 	| PUT 	  | /messages/1 |
| .patch() 	  | PATCH 	| /messages/1 |
| .remove() 	| DELETE 	| /messages/1 |

## First Service

As first I implemented the message service from the feathers tutorial without
authentication and local store.
To make my first tests I used curl and the "Postman" chrome application as REST client. The following curl commands has always an additional echo command to
prevent display problems in the terminal window.

The service will show that it's database is empty:

    $ curl -X GET http://localhost:3030/messages/ && echo
    {"total":0,"limit":10,"skip":0,"data":[]}

To add a message:

    $ curl -X POST http://localhost:3030/messages/ && echo
      -H 'Content-Type: application/json'
      --data-binary '{ "name": "Curler", "text": "Hello from the command line!" }'
    {"name":"Curler","text":"Hello from the command line!","_id":"UccphC13T4SBjBO6"}

Now the message is displayed, too:

    $ curl -X GET http://localhost:3030/messages/ && echo
    { "total":1,
      "limit":10,
      "skip":0,
      "data":[
        { "name":"Curler",
          "text":"Hello from the command line!",
          "_id":"UccphC13T4SBjBO6"
        }
      ]
    }

The message may be deleted again using it's ID:

    $ curl -X "DELETE" http://localhost:3030/messages/UccphC13T4SBjBO6
    {"name":"Curler","text":"Hello from the command line!","_id":"UccphC13T4SBjBO6"}

# Authentication

To make authentication easy and secure I checked different solutions and decided to
go with [JWT](https://auth0.com/docs/jwt). This allows to use stateless server cluster
and therefore is more stable and easy to scale.

The JWT defines a compact and self-contained way for securely transmitting information between parties as a signed JSON object.

## Authentication in the Server

On the server side I firstly added a local file based storage using [NeDB](https://github.com/louischatriot/nedb) as driver.
To get this working you first have to insert a user:

    $ curl -X POST http://localhost:3030/users
      -H 'Content-Type: application/json'
      --data-binary '{ "email": "info@alinex.de", "password": "secret" }'
    {"email":"info@alinex.de","_id":"8MM6RJPafKeJse9o"}

Now you may get the JWT:

    $ curl -X GET http://localhost:3030/authentication
      -H 'Content-Type: application/json'
      --data-binary '{ "strategy": "local", "email": "info@alinex.de", "password": "secret" }'
    {"accessToken":"eyJhbGciOiJIUzI1NiIsInR5cCI6ImFjY2VzcyJ9.eyJ1c2VySWQiOiIxNGtyWGJ0RnJaSTJ1VmJsIiwiaWF0IjoxNTE1NDIxMzQ2LCJleHAiOjE1MTU1MDc3NDYsImF1ZCI6Imh0dHBzOi8veW91cmRvbWFpbi5jb20iLCJpc3MiOiJmZWF0aGVycyIsInN1YiI6ImFub255bW91cyIsImp0aSI6IjFlZGZkODc0LWNlMWEtNDNkZS05OTRlLTI4MzI1NDRiZDFlYyJ9.Zwu5XxxNu5QC6K53j358rCXFyiPIFu5TlrKoohq7Khs"}

This access Token can now be used to access restricted services (I made the message service restricted for this, so the above without authentication won't work anymore):

    $ curl -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6ImFjY2VzcyJ9.eyJ1c2VySWQiOiIxNGtyWGJ0RnJaSTJ1VmJsIiwiaWF0IjoxNTE1NDI1NTg0LCJleHAiOjE1MTU1MTE5ODQsImF1ZCI6Imh0dHBzOi8veW91cmRvbWFpbi5jb20iLCJpc3MiOiJmZWF0aGVycyIsInN1YiI6ImFub255bW91cyIsImp0aSI6IjkyMGZhY2IwLWVmZTItNDc1MS1iNGJjLTYyNGFiNDNmZmRmNyJ9.x4jSVMIMpVV7j0_ei402DvckHWUcgi0xOiO9r2trY68'
      -X POST http://localhost:3030/messages

## Validation & Co

Therefore I added a hook for the message/before/create method. In which the given
data will be checked and sanitized.
Also user information like cration time and user reference may be added with such hook automatically.

## Combining information

Eith an after hook the returned information can be changed such as adding the user information directly to the user reference.

# Further steps

My next step will be to integrate the authentication through this server into the quasar client app.


_Alexander Schilling_
