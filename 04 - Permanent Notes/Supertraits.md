---
tags:
---
# Supertraits
Sometimes you may want to create traits that depend on other traits. In other words, you may come across situations where you want trait boundaries for traits. the boundary your trait depends on in this case is called a supertrait.

Adding trait boundaries to trait is similar to trait boundaries in generic types:
```rust
trait MyTrait: Supertrait {
	fn function(&self,...) {...}
}
```
For a type to implement `MyTrait`, it must implement `Supertrait` as well.

Consider, for, example, a print with outlines:
```rust
use std::fmt::Display;
trait OutlinePrint: std::fmt::Display {
	fn outline_print(&self) {
		let output = self.to_string();
		let len = output.len();
		println!("{}", "*".repeat(len + 4));
		println!("*{}*"), " ".repeat(len + 2));
		println!("* {} *", output);
		println!("*{}*"), " ".repeat(len + 2));
		println!("{}", "*".repeat(len + 4));
	}
}
```
here the supertrait is the `Display` trait, which is used so that `to_string()` method can be called automatically. if we try to implement this on our custom type that does NOT have the `Display` trait implemented, it will raise error.

---
Categories: 
References:
Created: 2024-05-27
