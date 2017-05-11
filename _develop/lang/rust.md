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
Ro get a full featured development system for Rust programming I did the following
steps.

### Install Rust

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

### Install Helper Tools

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

### Install Atom Editor Plugins

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


Learning
--------------------------------------------
To dive into I worked through the following resources:
- [The Rust Programming Language](http://rust-lang.github.io/book/second-edition)
  it includes some examples to develop


Test
---------------------------------------------
Rust has the following tests:
- unit tests
- integration tests

Both can be run using `cargo test`.


Automation
----------------------------------------------
[just](https://github.com/casey/just) is a build tool like `make` which runs commands,
produces detailed error messages and is less surprising than make. But you may
do all these steps on your own, too. Also most commands will output the real
shell calls which were done.

It needs a `justfile` within your project root which defines the possible commands.
Afterwards you may call `just <command>` from within your main directory. Some of
the commands also allow parameters.

The `alinex` projects use the following targets which are defined like under
[justfile](https://github.com/alinex/rust-operator/blob/master/justfile).

__Developing__:
- `check` for a faster compile to only check for correctness
- `test` to run all tests
- `testonly PATTERN` to test only specific library tests
- `run LOGLEVEL` to run in `debug`, `info` (default) or `error` mode
  you may also give `<PATH>[=<LEVEL>][,<PATH>[=<LEVEL>]]...`
- `outdated` to check for [outdated crates](https://github.com/kbknapp/cargo-outdated)
- `update` use newer package versions there possible
- `updateonly CRATE` only update the defined crate

__Finalizing__:
- `lint` to lint code using [clippy](https://github.com/arcnmx/cargo-clippy)
- `showdoc` create and open documentation in browser
- `doc` only update documentation

__Publishing__:
- `release` make a release file
- `publish` to finalize current version


Developing
---------------------------------------------

### Cargo

Cargo is used to manage the Rust packages which are in the [crates.io](https://crates.io)
package repository.

- `Cargo.toml` describes the dependencies
- `Cargo.lock` contains exact information about the used dependencies

To check for updates call `just outdated` and to update them `just update` or
`just updateonly <CRATE>`.

### Crates

Rust packages can be found in [crates.io](https://crates.io/search?q=just) and
all packages which are released there have there API documentation under
[docs.rs](https://docs.rs).

Some popular and useful packages are:
- [clap](https://clap.rs/) -
  cli interface and argument parser
- [iron](http://ironframework.io/doc/iron/) -
  http server


### Test

### Coverage

http://sunjay.ca/2016/07/25/rust-code-coverage

    apt-get install libcurl4-openssl-dev libelf-dev libdw-dev cmake gcc binutils-dev libiberty-dev
    wget https://github.com/SimonKagstrom/kcov/archive/master.tar.gz
    tar xzf master.tar.gz
    cd kcov-master
    mkdir build
    cd build
    cmake ..
    make
    sudo make install

    kcov --exclude-pattern=/.cargo,/usr/lib --verify target/cov target/debug/operator-*
    ￼xdg-open target/cov/operator-*/index.html


Coding
-----------------------------------------------
If you use linting through `clippy` you may ignore a warning at one point. To do
this use the following syntax which is only read on the `cargo clippy` call which
is also run using `just link` in the alinex projects:

``` rust
#[cfg_attr(feature = "cargo-clippy", allow(needless_pass_by_value))]
fn is_u32(v: String) -> Result<(), String> {
    if v.parse::<u32>().is_ok() {
        return Ok(());
    }
    Err(format!("{} isn't a positive integer number", &*v))
}
```


Finalizing
---------------------------------------------

- lint
- travis

### Documentation

Documentation is written as markdown within or before the element to document.

Generate documentation and open in browser using `cargo doc --open`.


Publishing
---------------------------------------------

### Release

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
