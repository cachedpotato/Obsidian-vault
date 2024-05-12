---
tags:
  - Rust
---
## Common types
1) Tuples
```rust
let tup: (i32, u8, char) = (-3, 5, 'a');

//deconstruction
let (x, y, z) = tup;
println!("tuple deconstruction: {x}, {y}, {z}");
println!("this is also possible: {tup.0}, {tup.1}, {tup.2}");

let empty = () //denotes empty value/return type
```

2) Arrays
``` rust
//arrays are fixed in size
//elements must be of the same type
let a: [i32; 5] = [1, 2, 3, 4, 5]; 

println!("first element: {a[1]}");
//invalid indexes will give RUNTIME error
```

3) usize
usize is an unsigned integer with a "dynamic" size that differs by the architecture of the computer. for x86_64 it's going to be u32, for aarch_64 it's going to be u64, etc.
```rust
let u: usize = 9;
//this takes the same amount of space in my computer
let u2: u32 = 9; 
```

4) byte literal
```rust
let bs: 
let s = b' ' //byte literal of whitespace

```

5) slice type
``` rust
let a: [u8;5] = [1, 2, 3, 4, 5];
let slice = &a[1..4];
assert_eq!(slice, &[2, 3, 4]);
```
slices are a reference to a preexisting array. slice types, as seen in the representation, **IS NOT MUTABLE**. think of string literal, which is also a type of slice.

## Types with multiple values

6) [[Enum]]

7) [[Structs]]

## Collections
Collections can contain multiple values. Unlike the built-in array and tuple types, these are stored in the [[Heap]]. Common collections include:
- [[String in Rust]]
- [[Vector in Rust|Vector]]
- [[Hash Map in Rust|Hash Map]]



---
Categories: [[Rust]], [[Data Types]]
References:
Created: 2024-05-09