---
tags:
---
# Rust Error E0716
Consider this implementation of Cons:
``` rust
enum List<'a> {
	Cons(i32, Box<&'a List<'a>>),
	Nil,
}
use List::{Cons, Nil};
fn main() {
	let a: List = Cons(5, Box::new(&Cons(10, Box::new(&Cons(Nil)))));
	let b: List = Cons(5, Box::new(&a));
}
```
Doing this gets us this error:
```
error[E0716]: temporary value dropped while borrowed
 --> src/main.rs:7:35
  |
7 |   let a: List = Cons(5, Box::new(&Cons(10, Box::new(&Nil))));
  |                                   ^^^^^^^^^^^^^^^^^^^^^^^^  - temporary value is freed at the end of this statement
  |                                   |
  |                                   creates a temporary value which is freed while still in use
8 |   let b: List = Cons(3, Box::new(&a));
  |                                  -- borrow later used here
```
This is because when we just use ```&Cons(10, ...)```, because this is not an explicit name of a variable, Rust considers it to be temporary. using it like this is essentially the same as the following: 
``` rust
let a: List = Cons(5, Box::new(
	{
		let tmp = Cons(10, ...); //shortened for the sake of brevity
		&tmp
	}
));
```
This is a case of a dangling reference, which is a memory risk and something that Rust will raise a compiler error over.

To fix this, we need to use a let binding, like so:
``` rust
let nil: List = Nil;
let l10: List = Cons(10, Box::new(&nil));
let a: List = Cons(5, Box::new(&l10));
let b: List = Cons(3, Box::new(&a));
let c: List = Cons(4, Box::new(&a));
```

---
Categories: [[Error Handling in Rust]]
References:
Created: 2024-05-17
