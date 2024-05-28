---
tags:
---
# The ! Type
The `!` type is called the _never_ type and as the name suggests, it returns nothing. It may seem useless to even have this, but this type has one really cool feature - it can be coerced into _any_ type. We've actually seen a pretty common use case of this: `continue`.

```rust
let guess: i32 = match guess.trim().parse() {
	Ok(n) => n,
	None => continue,
}
```
`guess` is of type `i32`, and by design match CANNOT return different types of values. But for the None arm we have `continue`, which returns nothing and just moves on to the latter part of the code. This is possible because 
- continue is a `!` type which returns nothing
- the `!` type here was coerced into `i32` 

Other examples of the never type include:
1) The `panic!` macro
``` rust
impl <T> Option<T> {
	pub fn unwrap(self) -> T {
		match self {
			Some(val) => val,
			None => panic!(...)
		}
	}
}
```

2) `loop`
``` rust
loop {
	println!("this goes on forever and returns nothing")
}
```

---
Categories: [[Rust Types]]
References:
Created: 2024-05-28
