---
tags:
---
Cargo is the package manager for [[Rust]]. The following are basic commands of cargo:

``` rust
cargo init //creating a new crate from preexisting directory
cargo new //creating create from scratch
cargo check //DOES NOT CREATE EXECUTATBLE. For testing purposes
cargo build //for creating executable
cargo run //for creating and running executable
```

a crate can be thought of as a project folder.
- cargo.lock stores version info of rust, dependencies, etc. This is to ensure easy reproducibility. ^85589b
- [[Cargo TOML |cargo.toml]] stores dependencies

### Cargo build
```rust
cargo build //no optimization, in target/debug
cargo build --release //optimized, in target/release
```

---
Categories: [[Cargo]]
Created: 2024-05-09