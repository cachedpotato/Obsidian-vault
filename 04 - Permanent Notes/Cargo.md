---
tags:
---
# Cargo
we already talked about the [[Cargo Basics|basics of cargo]] before, but let's get more in depth now.

## Release profiles
cargo has two main profiles, and each serve a different purpose. set ```opt-level``` (optimization level) accordingly
### dev profile
mainly used for development. the profile used when running ```cargo build```.
``` rust
[profile.dev]
opt-level: 0
```
the optimization isn't really necessary for debugging/development, so we're better off not letting the compiler optimize the code. Indeed, this is the default setting for dev profile.

### release profile
mainly used for release builds, a la ```cargo build --release```. We're trying to actually _release_ what we made here, so optimization is necessary. The default opt-level is 3, which is the maximum level.

## Crates.io
once you make a crate, or want to download a package, you can use [[Crates.io]]. this site is the main repository for Rust crates, and is mostly open source.

## Cargo Workspace
As your project gets bigger, you may want to split your package not just into modules, but into separate crates, and merge them all into one later. Cargo offers a feature called [[Cargo Workspace|workspace]] that does just that. This way multiple packages related to a single project can be developed in tandem.

## Cargo install
to install binaries in crates.io, get its name and simply do the following:
``` bash 
cargo install [name]
```




---
Categories: [[011-Rust]]
References:
Created: 2024-05-16
