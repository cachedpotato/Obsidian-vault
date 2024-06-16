---
tags:
---
# Function Pointers in Rust
In rust we can pass closures, which are unnamed functions, into functions using the `Fn` family of traits, like so:
``` rust
fn passes_closure<F>(x: i32, f: F) -> i32
where
	F: FnOnce(i32) -> i32,
{
	f(x)
}
fn main() {
	let x: i32 = 5;
	let c = |n| n + 1;
	assert_eq!(passes_closure(x, c), 6);
}
```
But what if we want to pass named functions and not just closures? Rust has you covered - we have function pointers! the function pointer _type_ is `fn`. Don't get confused with the `Fn` _trait!_

``` rust
fn do_twice(f: fn(i32) -> i32, x: i32) -> i32 {
	f(x) + f(x)
}
fn add_one(x: i32) -> i32 {
	x + 1
}
fn main() {
	let x: i32 = 5;
	assert_eq!(do_twice(add_one, x), 12);
}
```

We've mentioned the `Fn` traits before - `fn` type actually implements all three of the closure traits, meaning you can pass a function pointer as an argument to a function that takes in a closure!
``` rust
fn main() {
	// -- snip
	assert_eq(passes_closure(x, add_one), 6);
}
```
here the `add_one` acts as the function pointer, which has the signature `fn(i32) -> i32`. This means there are now two ways of doing things - using closures or function traits. take `map` for example.

```rust
enum Status {
	Value(u32),
	Stop,
}

fn main() {
	let status_list: Vec<Status> =
		(0u32..20).map(|n| Status::Value(n)).collect();
	let status_list2: Vec<Status> = 
		(0u32..20).map(Status::Value).collect();
}
```
Here we used the Enum variants as initializer function. 

## Returning Closures
Remember, closures are anonymous functions that implements the `Fn` _traits_, meaning wanting to return a closure is the same as wanting to return a [[Trait Objects|trait object]]. recall that trait objects are [[Dynamically Sized Types|DSTs]]:
```rust
fn returns_closure() -> Box<dyn Fn(i32) -> i32> {
	Box::new(|x| x + 1)
}
```
therefore you should wrap it with a pointer.



---
Categories: [[011-Rust]]
References:
Created: 2024-05-28
