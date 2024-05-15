---
tags:
---
# Unwrap
Here are some notable Unwrap functions and its usages.
### unwrap
```rust
fn main() {
	//some code regarding vectors....
	let n: String = v.get(100).clone().unwrap();
}
```
unwrap is for... well, unwrapping values inside a wrapper. For example, if you unwrap an ```Option<T>```, you'd get T on successful attempt. the code will panic if said Option is None. Similar to expect, this can be used for testing.


## ```unwrap_or```

```rust
fn test(x: i32) -> Result<String, &'static str> {
	if x > 0 {return Ok(String::from("is positive"))}
	Err("x is negative")
}

fn main() {
	let x = -2;
	let y: String = text(x).unwrap_or(String::from("not the Err"));
}
```
```unwrap_or``` returns a "default" value upon getting the Err variant of Result. Therefore, it will not print out the error message ```x is negative``` when assigning y.

## ```unwrap_or_else```

```rust
use std::programs;
let n: Config::build(&args).unwrap_or_else(|err| {
	println!("{err}"); //for str/String error types
	programs.exit(1); //exit with error code
});
```
```unwrap_or_else``` takes a [[Closure|closure]] as input to handle error cases, which is more elegant than straight-up panicking as is the case with ```unwrap```. 


---
Categories: [[Rust]] 
References:
Created: 2024-05-15
