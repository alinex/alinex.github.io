---
title: Rust
layout: develop
---

_My first experience with rust!_

I decided to dive into a new language, a compiler language this time. So I decided between
`Go` and `Rust`. This document describes the result of my experience.


Installation
--------------------------------------------
I installed it on my local machine using:

    $ curl https://sh.rustup.rs -sSf | sh

The installation told me that it will use the directory `/home/alex/.cargo/bin` for
the new binaries and will add this to my profile's search path.
But it only did so for `.profile` so I had to add it to `.bashrc` the same way by hand.

That was all.


Setup
--------------------------------------------
As editor I firstly use Atom with the following additional packages:
- language-rust
- linter-rust
- rust-api-doc-helper
