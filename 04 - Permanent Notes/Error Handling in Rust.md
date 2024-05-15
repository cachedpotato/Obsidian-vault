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
Because panicking crashes your program, you should use it wisely. A good situation to use ```panic!``` would be cases where continuing the program would put it or even your computer in jeopardy. 

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

## Custom Types for Error handling
Sometimes we encounter cases where a certain variable **MUST** meet several conditions, which are not possible by using the primary types alone. For example, we may want a variable to be of size between 1 and 100. Whenever this variable this gets passed to a function, we need to take care of cases where the variable goes out of range. This can be cumbersome.

What we can do, then, is to create a new type, either with struct or enum, and put limitations there.
```rust
struct Guess {
	value: i32,
}
impl Guess {
	pub fn new(value: i32) -> Guess {
		if value < 1 || value > 100 {panic!("Guess out of range");}
		Guess{ value }
	}

	pub fn value(&self) -> i32 {
		self.value
	}
}
```

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
it's better to use expect() than do nothing, but in will panic if an error occurs. Use this for super simple stuff or for testing.

## [[Unwrap]] family of functions
Because Rust's most defining features include Options and Result, which are both wrapper enums, Rust provides a plethora of functions that deal with wrapping/unwrapping of such values. 

### ?
```rust
use std::error::Error;
fn run(x: Config) -> Result<(), Box<dyn Error>> {
	//snip
	let test: String = x.stuff_that_returns_Result()?;
}
```
In this case, the ? operator will return the exit the run function with Err variant as output upon failure. Note that to use ? we need to have the function return Result with Err variant having the ```Error``` trait.

---
Categories: [[Rust]], [[Debug]] 
References: 
Created: 2024-05-09