---
tags:
---
# Declarative Macros
This type of macro is the most used macro in Rust. you can declare one with `macro_rules name`, which, once exported, can be called with `name!`. Note that when we're declaring the macro we do not add the exclamation point. Here's a simplified version of the `vec!` macro:
``` rust
#[macro_export]
macro_rules! vec {
	($($x:expr), *) => {
		{
			let mut temp_vec = Vec::new();
			$(
				temp_vec.push($x);
			)*
			temp_vec
		}
	};
}
```
macros' pattern matching syntax is different from normal pattern matching, as it operates on the code structure and variable names itself rather than the expression/value. Here are some of the rules:

- `$` to declare a variable in the macro system that will contain the Rust code matching the pattern
- `$x:expr` matches any expression in the code and binds it to x
- `*` means a pattern can appear any amount of time

Now let's look at the `($($:expr), *) =>`. Using the information above, we can figure out that this macro is trying to bind a pattern of any `expression, ` and that can be repeated any amount of time. after the fat arrow sign we make a block were the actual code of the macro is written.

First, we make a temporary vector named `temp_vec`, then we repeat the `temp_vec.push($x)` command as many times as we need (hence the asterisk), which is the length of the input to our macro. Finally, we return the vector.

Macro arms are divided not with `,` but with semicolons `;`
```rust
macro_rules! my_macro {
	() => {
		println!("Check out my macro!");
	};
	($val:expr) => {
		pritntln!("Check out my other macro: {}", $val);
	}
}

fn main() {
	my_macro!();
	my_macro!(7777);
}

```



---
Categories: [[Rust Macros]]
References:
Created: 2024-05-28
