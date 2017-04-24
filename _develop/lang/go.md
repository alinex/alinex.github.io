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
# set path to go and compiled programs
echo "export PATH=$PATH:/usr/local/go/bin:~/go/bin" >> ~/.bashrc
echo "export PATH=$PATH:/usr/local/go/bin:~/go/bin" >> ~/.profile
export PATH=$PATH:/usr/local/go/bin:~/go/bin
```

Other installation methods also exist see the [Project Site](https://golang.org/doc/install).


Introduction
----------------------------------------------
As first introduction to learn the language you find everything under
[https://golang.org/doc](https://golang.org/doc) like the interactive Tout.

The main commands are:

    go build          # check if it can be compiled
    go install        # to build and make a runnable command
    go test           # run unit tests
    <name>            # to directly run it, because you have it in your path
    go get <path>     # fetch and install


File Structure
-----------------------------------------------
The go workspace (`~/go` under Linux) contains the following directories:

    src/                            # sources
      github.com/alinex/go-learn    # package source
        .git/                       # version control system
        ...
    pkg/                            # downloaded packages
    bin/                            # executable commands


Editor
----------------------------------------------------
At first I use the `Atom` editor with the folowing plugins:
- go-plus
- go-debug

No need forca styleguide here because formatting is done by`gofmt`
OOOn it's own.
