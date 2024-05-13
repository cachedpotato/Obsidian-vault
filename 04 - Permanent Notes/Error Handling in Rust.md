---
tags:
  - Rust
---
# Error Handling in Rust
Rust makes a distinction between two types of errors
- Recoverable error: Minor errors such as _file not found_ error
- Unrecoverable error: Major errors such as **Index Out of Bounds** error

Depending on the type of the error, you may want to implement different handling methods.

## Unrecoverable Error - ```panic!```
For unrecoverable errors, sometimes it's best for the program to completely halt. This is where the ```panic!``` macro comes in handy.
```rust
fn something_horrible() {
	panic!("write your error message here");
}

fn main() {
	something_horrible();
}
```

running this code will result in the program crash and will leave the following message:

```
$ cargo run
   Compiling panic v0.1.0 (file:///projects/panic)
    Finished dev [unoptimized + debuginfo] target(s) in 0.27s
     Running `target/debug/panic`
thread 'main' panicked at src/main.rs:
write your error message here
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
```

run with ```RUST_BACKTRACE=1 cargo run``` to see the full backtrace.

## Recoverable Error - Result
We've briefly looked at the Result [[Enum]] before, but let's go a bit deeper. Result enum have two variants: Ok() and Err(). We can do pattern matching with ```match``` for error handling, like so:

```rust
use std::io;
fn main() {
	let mut s: string = string::new();
	println!("enter a number!");
	match io::stdin().read_line(&s) {
		Ok(num) => num, //pass the number on success
		//throw error message on ANY error (_)
		Err(_) => panic!("yo that ain't a number"),
	}
}
```

_OH BUT WE CAN GO DEEPER_. add another layer of pattern matching to do more sophisticated error handling:
```rust
use std::fs::File;
use std::io::ErrorKind;

fn main() {
	let open_file_result = File::open("test.txt"); //returns Result
	let file = match open_file_result {
		Ok(f) => f,
		Err(error) => match error.kind() {
			ErrorKind::NotFound => match File::create("test.txt") {
				Ok(fc) => fc,
				Err(e) => panic!("problem creating file: {:?}", e)
			},
			other_error => {
				panic!("Problem opening the file: {:?}", other_error)
			}
		}
	};
}
```
Reminder that you can name the default case for match

## Functions/methods related to Error handling
### expect
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
### ?
```rust
```

---
Categories: [[Rust]]
References: 
Created: 2024-05-09