---
tags:
---
# @ Bindings
We use the `@` binding to get the exact value we matched with a range `..=` pattern or the `|` pattern.

``` rust
enum Message {
	Hello { id: i32 },
}

fn main () {
	let msg = Message::Hello {id: 5};
	match msg {
		Message::Hello {
			id: id_variable@1..=7
		} => println!("Hello message with id {}", id_variable),
		Message::Hello {
			id: id_or@(8|9|10)
		} => println!("Hello message with id or {}", id_or),
		Message::Hello{ id } => println!("another id {}", id),
	}
}
```
`var_name@range` is how you should use the @ bindings.
For the `|` pattern, we need to enclose it with parentheses.

---
Categories: [[Pattern Syntax in Rust]]
References:
Created: 2024-05-24
