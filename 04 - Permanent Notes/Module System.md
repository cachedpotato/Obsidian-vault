---
tags:
  - Rust
---
# Module System
Rust has a number of features that allows you to manage your code and is collectively referred to as the module system. The system includes:
- Packages: build/test/sharing crates
- Crates: tree of modules that creates a library/executable
- Modules/use: control scope, privacy of paths, etc.
- Paths: method of naming an item i.e struct, function, module...

## Crate
a _crate_ is the smallest amount of code that the Rust compiler considers at a time. Kinda like a unit I guess?
crates have two types:
- Binary: creates programs/executables. has main.rs
- Library: define functionality. no main.rs

## Package
a package is a bundle of one or more creates that provides a set of functionality.
A package contains a [[Cargo TOML]] file that describes how to build said crates. 
A package can
- have multiple binary crates
- have ONLY ONE library crate

## [[Modules]]
Besides the root file (main.rs and lib.rs), a crate can have other .rs files that contain various modules/functions. 

## [[Paths]]
path allows you to name items, and show Rust where to find an item in the module tree, just like paths in a filesystem.


## References

categories: [[011-Rust]]
Created: 2024-05-11