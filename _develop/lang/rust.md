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
curl https://sh.rustup.rs -sSf | sh
echo "source $HOME/.cargo/env" >> ~/.bashrc
source $HOME/.cargo/env
```

The installation told me that it will use the directory `/home/alex/.cargo/bin` for
the new binaries and will add this to my profile's search path.
But it only did so for `.profile` so I had to add it to `.bashrc` the same way by hand.

That was all and to update it later use `rustup update`.

But to get a full blown environment you may also need:

``` shell
rustup component add rust-src
cargo install rustfmt
cargo install Racer
```

And to update Rust later use: `rustup update`


Learning
--------------------------------------------
To dive into I worked through the following resources:
- http://rust-lang.github.io/book/second-edition


Editor
--------------------------------------------
As editor I firstly use Atom with the following additional packages:
- language-rust
- linter-rust
- rustfmt
- racer

You have to setup racer with:
- path to bin: /home/alex/.cargo/bin/racer
- path to rust src: /home/alex/.rustup/toolchains/stable-x86_64-unknown-linux-gnu/lib/rustlib/src/rust/src/


Documentation
---------------------------------------------
Generate documentation and open in browser using `cargo doc --open`.


Release
----------------------------------------------
To make a release you only have to use: `cargo build --release`

But to get a better optimized build which is smaller in size add the following
to `Cargo.toml`:

    [profile.release]
    lto = true        # default is false
    panic = 'abort'   # default is 'unwind'

This will enable the link time optimization and only includes the parts of the
libraries we really used.

If you want to make the resulting binary smaller you may remove the debug symbols
with: `strip <binary>`.
