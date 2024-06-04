---
tags:
---
# Rust Macros
Macros is what is often referred to as metaprogramming. Macros essentially is a code that writes code. Rust's macro system is quite complex, but it can be categorized into two categories.

1) [[Declarative Macros]]: with `macro_rules!`
2) [[Procedural Macros]]
	- Custom `#[derive]` macros
	- Attribute-like macros that define custom attributes
	- Function-like macros that looks like functions but acts on tokens.

Macros can be used to reduce the amount of (repeated) code, but at the cost of readability. Macros also must be defined and brought into scope BEFORE calling in a file.

## Macros in modules
when you define macros inside a module, you must annotate the module with `#[macro_use]` to be able to actually call the macro.
``` rust
#[macro_use]
mod macros {
	macro_rules! my_macro {
		() => {
			println!("This is a macro");
		}
	}
}

fn main() {
	my_macro!();
}
```

---
Categories: [[Rust]]
References:
https://veykril.github.io/tlborm/
https://doc.rust-lang.org/reference/macros-by-example.html
Created: 2024-05-28
