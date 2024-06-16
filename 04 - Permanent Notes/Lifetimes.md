---
tags:
  - Rust
---
# Lifetimes
Lifetimes ensure that references are valid as long as we need them to do. In its most basic form, lifetimes can be thought of as scopes, or at least that's how I understand it.

Most of the time, lifetimes are pretty obvious, hence why we did not even once annotate lifetimes before this chapter. However, there comes a time where the compiler (or even us) don't know the lifetime of a function output or a variable. Take this for an example:

``` rust
fn longest(x: &str, y:&str) -> &str {
	if x.len() > y.len() {x}
	else {y}
}
```
we take two string slices, and return another string slice. Remember, these are _REFERENCES_. There's one problem with this function: we don't know how long the output will last. Will it follow x? will it follow y? This cannot be determined during compile time. In times like this, we need to explicitly annotate lifetimes to variables, like so:

```rust
fn longest <'a> (x: &'a str, y: &'a str) -> &'a str {...}
```

The annotation looks a lot like generics. That's because lifetimes pretty much ARE one. Lifetimes are annotated with an apostrophe(').
Note that this does NOT mean all ```x, y``` and output lives the exact same length. The lifetime annotation means all given variables _LIVE AT MOST AS LONG AS THE LIFETIME 'a_. In the context of this function, this means that the output will live the same amount as the variable with the shortest lifetime between the two inputs.

Ultimately, lifetime syntax is about connecting the lifetimes of various parameters and return values of functions.

## Lifetimes in structs
if you want to have a reference as a value of a struct, you often times need to annotate lifetime

```rust
struct HasStringSlice <'a> {
	slice: &'a str,
}

fn main() {
	let stringz = String::from("This is a string");
	let word = stringz.split_whitespace.next().expect("no word");
	let w = HasStringSlice {
		slice: w,
	}
}
```

## Lifetime Elision
The compiler uses _three rules_ to infer lifetimes, and only in situations where the compiler CANNOT do we need to explicitly annotate. The three rules are as follows:

1) The compiler assigns one lifetime parameter per reference.
``` rust
fn test <'a> (a: &'a str) -> &str
fn test <'a, 'b> (a: &'a str, b: &'b str) -> &str
//so on and so forth
```

2) If there is exactly one input lifetime parameter, that lifetime is assigned to _ALL_ output lifetime parameters.
``` rust
fn test <'a> (a: &'a str) -> &'a str
```

3) If there are multiple input lifetime parameters, but one of them is ```&self || &mut self```, the lifetime of that is assigned to all output lifetime parameters.
``` rust
impl StringSliceStuff {
	fn test <'a, 'b> (&'a self, &'b other: &str) -> &'a str
}
```

if the compiler can assign lifetimes to all inputs and outputs, then we don't need to annotate them ourselves.

Now let's get back to that example where we HAD to annotate the lifetimes. Lets do this step by step.

``` rust
fn longest(x: &str, y: &str) -> &str

//step 1
fn longest <'a, 'b> (x: &'a str, y: &'b str) -> &str

//step 2 - DOES NOT APPLY HERE - MULTIPLE LIFETIMES
fn longest <'a, 'b> (x: &'a str, y: &'b str) -> &str

//step 3 - DOES NOT APPLY HERE - IS NOT A METHOD
fn longest <'a, 'b> (x: &'a str, y: &'b str) -> &str
```

we can see that the output lifetime parameter is not annotated after all 3 rules are considered. This is why the compiler threw an error.

## Lifetime annotations in Methods
Lifetime names for struct fields always need to be declared after the impl keyword and then used after the structs name.
```rust
impl<'a> ImportExcept<'a> {
	fn level(&self) -> i32 {...}
	fn announce_and_return_part(&self, announcement: &str) -> &str {...}
}
```

as for the second rule, because this is a method, the output's lifetime is the same as ```&self```'s. add in the second rule of lifetime elision and boom we have lifetime annotation for all parameters. This is why we don't need to annotate them ourselves. if we were to, however, it would look something like this:
``` rust
fn announce_and_return_part <'a, 'b> (&'a self, announcement: &'b str) -> &'a str {...}
```

## Static lifetime
static lifetime denotes that a reference _can_ live for the entire duration of the program. All string literals have the static lifetime, denoted like so:
```rust
let a: &'static str = "I am static";
```

## lifetime with generic types
Now lets merge all [[Generics in Rust|generic]] type and lifetime parameters into one
```rust
use std::fmt::Display;

fn longest_with_an_announcement<'a, T>(
	x: &'a str,
	y: &'a str,
	ann: T,
) -> &'a str 
where
	T: Display,
{
	println!("Announcement!: {}", ann);
	if x.len() > y.len() {
		x
	} else {
		y
	}
}
```
... all this for a goddamn function? Damn.


---
Categories: [[011-Rust]]
References:
Created: 2024-05-14