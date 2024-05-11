---
tags:
  - Rust
links: "[[Rust]]"
---
# Ownership
one can say this is THE DEFINING factor of Rust... But what the hell even is it?

ownership is a set of rules that govern how a rust program manages memory.
basically, instead of having a garbage collector, Rust _forces_ you to manage
memory through ownership & borrowing, and make sure your code is memory-safe.

When your code uses memory (or rather allocates) in the [[Stack|stack]], all is
good but problems happen once you allocate memory in [[Heap|heap]]. Allocating
memory and removing them is a hassle (looking at you C/C++), and often times lead to memory leakage. So the question is: How does Rust stop this?

## Ownership rules
There are a lot of stuff Rust do to ensure memory safety, but the crux of it comes down to the "ownership rule":
- Each value in Rust has an **owner**
- There can be **ONLY ONE OWNER** at any given time
- When the owner goes out of scope, the value will be dropped.

Having just one owner is not to say only one can access the variable. We can use [[Reference|references]] for that.

Other rules worth mentioning:
- Types stored in heap have the copy trait, so ownership won't move:
```rust
let x: u8 = 3;
let y = x;
println!("{x} and {y} both works");
```
Stack-stored types are the likes of u8, i32, usize, and tuples of said types.

## References

Created: 2024-05-09