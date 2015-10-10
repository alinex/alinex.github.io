---
title: SSH Tunneling
layout: post
tags: SSH Development
---

First I didn't plan to make a new module but as I needed the tunneling feature for
my [database](http://alinex.github.io/node-database/) I didn't found an appropriate
module on the net.
Within two days I got the planing, coding and testing ready and have a stable
version based on ssh2 module, now.

Tunneling Basics
----------------------------------------------------------------
A SSH tunnel consists of an encrypted tunnel created through a SSH protocol
connection. A SSH tunnel can be used to transfer unencrypted traffic over a
network through an encrypted channel. With such an SSH tunnel users may bypass
firewalls that prohibits or filter certain internet services. If users can connect to
an external SSH server, they can create a SSH tunnel to forward a given port on
their local machine to a host and port reachable only from the remote ssh
server.

This technology may also be used on the linux shell using the ssh call:

``` bash
ssh user@sshhost -L 8080:172.32.0.11:80 -N
```

His will establish a tunnel from the local port 8080 to 172.32.0.11:80
(reachable from sshhost).

This technology is also called __local port forwarding__. The reverse way of
a tunnel is called remote port forwarding and at last dynamic port forwarding will
forward all local ports.

Using the new Module
----------------------------------------------------------------
Using this module inside my database module was easy like described in the
README:

``` coffee
sshtunnel = require 'alinex-sshtunnel'
sshtunnel
  ssh:
    host: '65.25.98.25'
    port:  22
    username: 'root'
    #passphrase: 'mypass'
    privateKey: require('fs').readFileSync '/home/alex/.ssh/id_rsa'
    #localHostname: "Localost"
    #localUsername: "LocalUser"
    #readyTimeout: 20000
    keepaliveInterval: 1000
    #debug: true
  tunnel:
    host: '172.30.0.11'
    port: 80
    #localhost: '127.0.0.1'
    #localPort: 8080
, (err, tunnel) ->
    console.log "tunnel opened at #{tunnel.setup.host}:#{tunnel.setup.port}"
    # wait 10 seconds, then close the tunnel
    setTimeout ->
      tunnel.close()
      cb()
    , 10000
```

Because I got all the information from my [config](http://alinex.github.io/node-config)
it was easy to write as:

``` coffee
tunnel = (conf, cb) ->
  sshtunnel = require 'alinex-sshtunnel'
  sshtunnel
    ssh: conf.ssh
    tunnel:
      host: conf.server.host
      port: conf.server.port
  , (err, tunnel) ->
    return cb err if err
    cb null, tunnel.setup
```

That's all that is to do. So my integration was fast and successful and I may
go on with the features of the database class.


Features
----------------------------------------------------------------

Most features are under the hood:

- a free local port will be detected automatically
- ssh connections with user+pass or using keys
- reuse of the same ssh connection if multiple tunnels have to be created on the
  same server
- reuse the same tunnel if called multiple times


Future
----------------------------------------------------------------
I don't have much features here missing. Only a reverse tunnel should be possible
by given it by setup. This may be added later because it is not needed for me.

Best Regards

//Alex//