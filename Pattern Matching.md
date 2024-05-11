---
tags:
  - Rust
links: "[[Rust]]"
---
# Pattern Matching
There are multiple types of pattern matching but let's get the important ones out of the way first.

## match
```rust
let o: Option<u8> = Some(5);
match o {
	Some(n) => println!("this is something"),
	None => println!("this is nothing")
}
```
matches are verbose, but at a cost - it **MUST** be exhaustive. take an enum for example:
```rust
enum States {
	Alaska,
	Alabama,
	NewYork,
	Mississipi,
	Louisiana,
	Georgia,
}

impl States {
	fn alaska(a: States) {
		match a {
			States::Alaska => println!("This IS alaska"),
			States::Alabama => println!("This is alabama"),
			_ => println!("don't care but I have to specify")
		}
	}
}

fn main() {
	//or think of situations like this
	let config_max: Option<usize> = Some<39>;
	match config_max {
		Some(n) => println!("max: {n}"),
		None => (), //return nothing <- boilerplate shit
	}
}
```
See how annoying this can get? what if we just need one branch? enter ```if let```.

## if let
```rust
let config_max: Option<usize> = Some<39>;
if let Some(n) = config_max {println!("max: {n}")}; //nice
```
Think of if let as a _snippet_ of match, to be exact just one match arm. On the **LEFT HAND SIDE** is the pattern, and the **RIGHT HAND SIDE** is the variable. Don't get it confused!
```rust
let confusing: Result<u8, String> = Ok(8);
//if let PATTERN = VARIABLE {stuff}
if let Ok(n) = confusing {println!("Everything under control")};
```

## References

Created: 2024-05-11