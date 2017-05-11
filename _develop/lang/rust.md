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
cargo install racer
cargo install just
cargo install cargo-check
cargo install cargo-outdated
rustup override add nightly
cargo install clippy
rustup override remove
```


Learning
--------------------------------------------
To dive into I worked through the following resources:
- [The Rust Programming Language](http://rust-lang.github.io/book/second-edition)


Editor
--------------------------------------------
As editor I firstly use Atom with the following additional packages:
- language-rust
- linter-rust
- rustfmt
- racer
- autocomplete-racer
- atom-beautify
- build-cargo
- build
- platformio-ide-terminal
- dockblockr

You have to setup racer with:
- path to bin: /home/alex/.cargo/bin/racer
- path to rust src: /home/alex/.rustup/toolchains/stable-x86_64-unknown-linux-gnu/lib/rustlib/src/rust/src/

While the style of code is maintained using rustfmt on save of file, you have the
ability to specify the concrete style rules:
[Config rustfmt](https://github.com/rust-lang-nursery/rustfmt/blob/master/Configurations.md)

The `build` plugin is triggered using `F9`.

The [Rust Language Server](https://github.com/rust-lang-nursery/rls) looks great
but is not stable in the moment and missing a working atom plugin.


Test
---------------------------------------------
Rust has the following tests:
- unit tests
- integration tests

Both can be run using `cargo test`.


Documentation
---------------------------------------------
Documentation is written as markdown within or before the element to document.

Generate documentation and open in browser using `cargo doc --open`.


Release
----------------------------------------------
To get a better optimized build which is smaller in size add the following
to `Cargo.toml`:

    [profile.release]
    lto = true        # default is false
    panic = 'abort'   # default is 'unwind'

This will enable the link time optimization and only includes the parts of the
libraries we really used.

To release at [crates.io](https://crates.io) you have to login there and copy
the API Access Token from cour [Account Settings Page](https://crates.io/me) using
`cargo login`. Once this is done you may run `just publish` (see below) or do these
steps on your own.

__Manual publish__

To make a release you have to use: `cargo build --release`.

If you want to make the resulting binary smaller you may remove the debug symbols
with: `strip <binary>`.


Make Tool
----------------------------------------------
[just](https://github.com/casey/just) is abuild tool like make which runs commands
produces detailed error messages and avoids make's idiosyncrasies to be easy to
debug and less surprising than make.

Install just using: `cargo install just`

It needs `justfile` which defines the possible targets in the main directory.
Afterwards you may call `just <target>` from within your main directory.

The alinex projects use the following targets:

- `run LOGLEVEL` to run in `debug`, `info` (default) or `error` mode
  you may also give `<PATH>[=<LEVEL>][,<PATH>[=<LEVEL>]]...`
- `test` to run all tests
- `testlib PATTERN` to test only specific library tests
- `check` for a faster compile to only check for correctness
- `build` to check if it can be build
- `lint` to lint code using [clippy](https://github.com/arcnmx/cargo-clippy)
- `outdated` to check for [outdated crates](https://github.com/kbknapp/cargo-outdated)
- `showdoc` create and open documentation in browser
- `doc` only update documentation
- `release` make a release file
- `publish` to finalize current version
- `nightly` to switch to nightly rust
- `stable` to switch back to stable


Packages
----------------------------------------------
Rust packages can be found in [crates.io](https://crates.io/search?q=just).

Some popular and useful packages are:
- clap - cli interface and argument parser
- just - make alternative


Coding
-----------------------------------------------
If you use linting through `clippy` you may ignore a warning at one point. To do
this use the following syntax which is only read on the `cargo clippy` call which
is also run using `just link` in the alinex projects:

    #[cfg_attr(feature = "cargo-clippy", allow(needless_pass_by_value))]
    fn is_u32(v: String) -> Result<(), String> {
        if v.parse::<u32>().is_ok() {
            return Ok(());
        }
        Err(format!("{} isn't a positive integer number", &*v))
    }
