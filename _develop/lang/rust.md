---
title: Rust
layout: develop
---

_My first experience with rust!_

In my effort to learn a new language I started to checkout `Go` and `Rust` both for
some days and do a bit in both to decide which one to choose for a deeper experience.
I worked a lot with Java later with NodeJS but both have some problems
for me. Java is not after my liking, while NodeJS is great for fast prototyping but
get problems if the project grows really big.

So in this article I describe the findings of `Rust` as an notebook for myself.


Installation
--------------------------------------------
To install the latest version of rust under Linux call:

``` shell
$ curl https://sh.rustup.rs -sSf | sh
echo "source $HOME/.cargo/env" >> ~/.bashrc
source $HOME/.cargo/env
```

The installation told me that it will use the directory `/home/alex/.cargo/bin` for
the new binaries and will add this to my profile's search path.
But it only did so for `.profile` so I had to add it to `.bashrc` the same way by hand.

That was all.


Learning
--------------------------------------------
To dive into I worked through the following resources:
-


Setup
--------------------------------------------
As editor I firstly use Atom with the following additional packages:
- language-rust
- linter-rust
