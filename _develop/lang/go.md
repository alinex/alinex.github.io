---
title: Go
layout: develop
---

_My first experience with go!_

After a short checkup of `Rust` I come to the conclusion `Go` is the new language
to dive into. I worked a lot with Java later with NodeJS but both have some problems
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

No need for a style guide here because formatting is done by`gofmt`
on it's own on saving.

To show your documentation in the browser star the godoc server:

    godoc -http=:6060 &       # to start it in the background

And then go in your browser to
[http://localhost:6060/pkg/github.com/alinex/go-learn/](http://localhost:6060/pkg/github.com/alinex/go-learn/).
