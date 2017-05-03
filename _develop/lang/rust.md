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
cargo install just
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

While the style of code is maintained using rustfmt on save of file, you have the
ability to specify the concrete style rules: https://github.com/rust-lang-nursery/rustfmt/blob/master/Configurations.md


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


Build Tool
----------------------------------------------
[just](https://github.com/casey/just) is abuild tool like make which runs commands
produces detailed error messages and avoids make's idiosyncrasies to be easy to
debug and less surprising than make.

Install just using: `cargo install just`

It needs `justfile` which defines the possible targets in the main directory.
Afterwards you may call `just <target>` from within your main directory.
