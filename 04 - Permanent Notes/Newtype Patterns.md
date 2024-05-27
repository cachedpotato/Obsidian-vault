---
tags:
---
# Newtype Patterns
By making a light wrapper around an external type, we can implement external trait on said type, bypassing the orphan rule. This wrapper is called a `Newtype`. For example, we can implement the `Display` trait to `Vec<T>` like so:
``` rust
use std::fmt;
struct Wrapper(Vec<String>);
impl fmt::Display for Wrapper {
	fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
		write!(f, "[{}]", self.0.join(","))
	}
}
fn main() {
	let w: Wrapper = Wrapper(vec![String::from("hello"), String::from("world")]);
	println!("{}", w);
}
```
we can unwrap the wrapper simply by calling `self.0`.

---
Categories: [[Advanced Traits]]
References:
Created: 2024-05-27
