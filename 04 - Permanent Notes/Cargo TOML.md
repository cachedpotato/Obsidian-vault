---
tags:
  - Rust
links: "[[Rust]]"
---
Rust manages package dependencies with cargo.toml. A few syntax to note:
```toml
rand = "0.8.5" 
rand = "^0.8.5"
```
the two are the same thing. Carrot sign implies the version must be higher than 0.8.5 but below 0.9.0.

## References

Created: 2024-05-09