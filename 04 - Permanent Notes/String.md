---
tags:
  - Rust
links:
---
## String and ```String```

What? what do you mean? Well, I mean this:
```rust
//this is a string LITERAL. This ain't mutable
let a = "hi"; 
//this is the CLASS String. This IS mutable
let mut b = String::from("hi")
```
String literals are your run-of-the-mill strings you see in other languages. Not in Rust. string literals aren't mutable! if you want to change a string literal, you must make it into a ```String``` class either via ```String::from()``` or ```to_owned()```. You can also change ```Strings``` by passing its reference to a function:

```rust 
fn main() {
	let mut s: string = string::from("init");
	elongate(s);
	println!("s has been appended: {s}");
}

fn elongate(s: &mut String) {
	s.push_str("appended");
}
```

## String Slice
string slice is represented as follows:
```rust
let s: String = String::from("this is a string");
//string slice is an array
let sslice: &str = &s[1..3] //prints "is"
let slice: &str = "wait string literal is a string slice?"
```
string slices are also pointers that points to a string. string slice has with it the pointer and the length. so if for example our string slice is ```&s[3..5]``` of string s, then the slice is a pointer that points to index 3 of s and has the length 2.

String literals are considered string slices. Reminder that string literals weren't mutable. That means _string slices aren't mutable as well_. The good thing about string slices is that if a function takes a string slice as its parameter, it will work on &String as well!
```rust
fn main() {
	let s: String = String::from("hello");
	let s_lit = "hello";
	println!("{first_three_char(s_lit)}");
	println!("{first_three_char(s)}"); //this works too!
}

fn first_three_char(s: &str) -> &str {
	&s[..3]; //index 0, 1, 2
}
```


## References

Created: 2024-05-09