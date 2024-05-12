---
tags:
  - Rust
---
# Modules
while there isn't a said rule for organizing modules, the Rust book provides a useful cheat sheet that can serve as a great starting point.
## Modules cheat sheet
1) **Start from the crate root**: The compiler first looks at the root file to get which codes to compile
2) **Declare modules in root**: use the keyword ```mod``` for declaring modules. the compiler will look for code in one of the tree places:
- Inline 
- file src/modname.rs
- file src/modname/mod.rs
Reminds me of how NixOS configs are split and stored in seperate directories/files.
3) **Declaring Submodules**: similar to modules, you can declare submodules. The compiler will look for the submodule's code in three places:
- Inline
- src/modname/submodulename.rs
- src/modname/submodulename/mod.rs
4) **paths to code in modules**: as long as privacy rules allow, once a module is part of your crate, you can refer to code in that module from anywhere.
5) [[Private and Public|Private vs Public]]: Code within a module is **PRIVATE BY DEFAULT**. use they key ```pub``` to make it (or its methods) public. 
6) **the [[Use|use]] keyword**: ```use``` keyword is used to create shortcuts to items to reduce repetition.
```rust
//if no use:
let a: crate::garden::vegetables::Asparagus = crate::garden::vegetables::Asparagus;

//with use:
use crate::garden::vegetables::Asparagus
let a: Asparagus = Asparagus
//remember using std::io?
```

## References

categories: [[Rust]]
Created: 2024-05-11