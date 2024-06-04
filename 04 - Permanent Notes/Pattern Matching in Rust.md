---
tags:
---
# Pattern Matching in Rust
Patterns are a special syntax in Rust for matching against the structure of types. A pattern consists of some combination of the following:

- Literals
- Destructured arrays, enums...
- Variables
- Wildcards
- Placeholders

We then use ```match``` to match/extract such patterns.
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
We can use the ```_``` pattern to match anything, but this is still cumbersome in some cases. What if we just need one branch? enter ```if let```.

## match and ownership
just like loops, pattern matching will take ownership:
```rust
struct Point {
	x: i32,
	y: i32
}
fn main() {
	let y: Option<Point> = Some(Point {x: 10, y: 10});
	match y {
		Some(p) => {println!("coord: {}, {}", p.x, p.y)},
		_ => println!("no point detected"),
	}
}
```
running this will give this compiler error:
```
error[E0382]: use of partially moved value: `y`
  --> exercises/options/options3.rs:18:5
   |
15 |         Some(p) => println!("Co-ordinates are {},{} ", p.x, p.y),
   |              - value partially moved here
...
18 |     y; // Fix without deleting this line.
   |     ^ value used here after partial move
   |
   = note: partial move occurs because value has type `Point`, which does not implement the `Copy` trait
help: borrow this binding in the pattern to avoid moving the value
   |
15 |         Some(ref p) => println!("Co-ordinates are {},{} ", p.x, p.y),
   |              +++

error: aborting due to 1 previous error

For more information about this error, try `rustc --explain E0382`.
```
The rust compiler kindly recommends a solution: borrow the binding using the `ref` keyword:
``` rust
//--snip
	Some(ref p) => {println!("{} {}", p.x, p.y)},
	//--snip
```

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
```if let``` can also use shadowed variables like ```match``` can:
``` rust
let age: Result<i32, _> = "32".parse();
if let Ok(age) = age {println!("age: {}", age);}
```

## While let conditional loops
We can use something similar to ```if let``` for looping. For example, we can iterate over some iterator with a method that returns an Option or a Result, like so:
``` rust
fn main() {
	let v: Vec<i32> = vec![1, 2, 3, 4, 5];
	while let Some(top) = v.pop() {
		println!("at the top: {}", top);
	}
}
```

## for loops
Remember, patterns isn't all literals and variables. it can also be deconstructions.
``` rust
fn main() {
	let v: Vec<i32> = vec![1, 2, 3, 4, 5];
	for (idx, val) in v.iter().enumerate() {
		println!("{}: {}", idx, val);
	}
}
```

## let
yes. _THAT_ let we've used countless times to declare variables.
``` rust
let x = 5; //let PATTERN = EXPRESSION
```
This is the reason why destructuring are even possible
``` rust
let (x, y, z) = (1, 3, 5);
```
because the left hand side is considered pattern, we can assign values to each variables.

## function parameters
The input parameters in functions are also patterns!
``` rust
fn pattern(&(x, y): &(i32, i32)) {
	println!("x: {}, y: {}", x, y);
}
fn main() {
	let point: (i32, i32) = (1, 2);
	pattern(&point);
}
```


---
Categories: [[Rust]]
References:
Created: 2024-05-24
