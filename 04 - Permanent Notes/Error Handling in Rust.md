---
tags:
  - Rust
---
# Types of error Handling

1) expect
```rust
use std::io;
fn main() {
	let mut s: string = string::new();
	println!("enter a number!");
	let n: u32 = io::stdin().read_line(&s)
		.expect("yo that ain't a number");
}
```
it's better to use expect() than do nothing, but in will panic if an error occurs. Use this for super simple stuff.

2) match
```rust
use std::io;
fn main() {
	let mut s: string = string::new();
	println!("enter a number!");
	let n: u32 = match io::stdin().read_line(&s) {
		Ok(num) => num, //pass the number on success
		//throw error message on ANY error (_)
		Err(_) => println!("yo that ain't a number"),
	}
}
```

3) ?
```rust
```
## References

categories: [[Rust]]
Created: 2024-05-09