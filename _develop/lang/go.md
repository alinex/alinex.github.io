---
title: Go
layout: develop
---

_My first experience with go!_

In my effort to learn a new language I started to checkout `Go` and `Rust` both for
some days and do a bit in both to decide which one to choose for a deeper experience.
I worked a lot with Java later with NodeJS but both have some problems
for me. Java is not after my liking, while NodeJS is great for fast prototyping but
get problems if the project grows really big.

So in this article I describe the findings of `Go` as an notebook for myself.


Installation
--------------------------------------------
This is done really easy under Linux:

``` shell
# download
wget https://storage.googleapis.com/golang/go1.8.1.linux-amd64.tar.gz
# install
sudo tar -C /usr/local -xzf go1.8.1.linux-amd64.tar.gz
# set path
echo "export PATH=$PATH:/usr/local/go/bin" >> ~/.bashrc
echo "export PATH=$PATH:/usr/local/go/bin" >> ~/.profile
export PATH=$PATH:/usr/local/go/bin
```

Other installation methods also exist see the [Project Site](https://golang.org/doc/install).


Introduction
----------------------------------------------
As first introduction to learn the language you find everything under
[https://golang.org/doc](https://golang.org/doc) like the interactive Tout.
