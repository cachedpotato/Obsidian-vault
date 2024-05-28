---
tags:
---
# Dynamically Sized Types
Compiler must know the size of each type for it to properly allocate memory. However, there are some cases where we do not know the exact size of a type at compile time. This is called Dynamically Sized Types (DST). One example is `str`:

```rust
let s1: str = "Hello world";
let s2: str = "How's it going?";
```
This, will in fact, NOT COMPILE! Because string literals can have massively different sizes, we can't create a variable holding a DST. However, what we can do, is create a pointer that points to said DST in heap:
``` rust
let r1: &str = "Hello world";
let r2: &str = "How's it going?";
```
pointers have a fixed size of `usize`, so the compiler can allocate memory for said pointer. Recall that this was also called a string slice. slices are a special pointer that 1) stores the address of the value it points to and 2) records the size (length) of the slice. The rules of dynamically sized types can then be summarized into one sentence:

> Put them behind a pointer!

Besides slices mentioned above, we've also seen another example of DST, which are [[Trait Objects]]:
``` rust
fn returns_result(x: i32) -> Result<i32, Box<dyn std::io::Error>> {}
```
We want to make space for a type that implements a certain trait, but we don't know exactly what type will implement that. So we put it behind a pointer, and DST is now able to compile. Note that Dynamic dispatch and use of DST may hinder performance.

## the Sized trait

To work with DST's rust provides the `Sized` trait to determine whether or not the type's size is known at compile time. Every generic types implement this trait by default.
```rust
fn generic_function<T: Sized>(x: T) -> T {...}
```
If we don't know whether the size will be known at compile time, we add a `?` in front of it, like so:
```rust
fn generic_function<T: ?Sized>(x: &T) -> T {...}
```
Note that the DST rules apply here, thus we need to pass the _pointer_ to the generic value and not the value itself.

---
Categories: [[Traits in Rust]]
References:
Created: 2024-05-28
