---
tags:
---
# Rust Error E0506
Besides the number available immutable/mutable references, there are restrictions to the lifetime of references.

Consider this example:
``` rust
let mut x: i32 = 3;
let y: &i32 = &x
println!("y is borrowing x: {y}, with address: {:p}", y);
x = *y + 1;
println!("Is y still valid? {y}"); 
```

This seems harmless, but when we try to compile, we get this error:
```
let y = &x;
  |     -- `x` is borrowed here
5 |   println!("y is borrowing x: {y}, with address" {:p}", y);
6 |   x = *y + 1;
  |   ^^^^^^^^^^ `x` is assigned to here but it was already borrowed
7 |   println!("Is y still valid? {y}");
  |                                - borrow later used here
```
This is _NOT_ a matter of mutability of y. It's a matter of the value of x being changed _WHILE Y IS STILL ALIVE_. While we can change values pointed by a reference using ```&mut```, that doesn't mean references expect the underlying value to change under the hood.

Even if a reference is a mutable one, if the reference is still valid and the value changes by some other measure, Rust will throw an error.

---
Categories: [[Error Handling in Rust]]
References:
Created: 2024-05-17
