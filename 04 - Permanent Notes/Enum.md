---
tags:
  - Rust
links:
---
### Option
```rust
enum Option<T> {
  Some(T),
  None,
}
```
Option takes care of the "billion dollar mistake", which is the null value, or lack there of. Everything will be either _something_, or _nothing_, simple as that.

### Result
Result is an enum with 2 types:
```rust
enum Result<T> {
  Ok(T),
  Err,
}
```

If some function returns a result, it's best practice to do [[Error Handling]], which is basically taking care of error cases.

Created: 2024-05-09