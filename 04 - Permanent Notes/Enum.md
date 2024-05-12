---
tags:
  - Rust
---
# Enum
enum is a type that can be one of a given set of types. types within enum can be pretty much anything.
```rust
enum Message {
	Quit, //unit struct
	Write(String), //tuple struct
	ChangeColor(u8, u8, u8), //tuple struct,
	Position {x: i32, y: i32}, //struct	
}

fn main() {
	let m: Message = Message::Write(String::from("Hello"));
	//println!("{m}") <- does not work because it does not have
	//display trait
}
```

## Implementation

```rust
impl Message {
	fn call(&self) {
		match self {
			Message::Quit => println!("quitting"), //LAMBDA BOIS
			Message::Write(s) => println!("wrote {s}"),
			_ => println!("hello")
		}
	}
}

fn main() {
	let m: Message = Message::Write(String::from("hello"));
	m.call(); //will print "write hello" in stdout
}
```

## Notable Enums

There are many ways enums can be used, but here are some great enums that are included in the prelude. Option takes care of the null problem and Result is used for error handling.
### Option
```rust
enum Option<T> {
  Some(T),
  None,
}
```
Option takes care of the "billion dollar mistake", which is the null value, or lack there of. Everything will be either _something_, or _nothing_, simple as that.

### Result
Result is an enum with 2 types:
```rust
enum Result<T> {
  Ok(T),
  Err,
}
```

If some function returns a result, it's best practice to do [[Error Handling in Rust]], which is basically taking care of error cases.


categories: [[Rust]], [[Data Types]]
Created: 2024-05-09