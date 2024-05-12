---
tags:
  - Rust
---
# String in Rust
Strings in Rust is pretty complicated. For starters, what you call string in other languages are called string _LITERALS_, and Rust has a separate class ```String``` for your normal string-like stuff.
## String and ```String```

What? what do you mean? Well, I mean this:
```rust
//this is a string LITERAL. This ain't mutable
let a = "hi"; 
//this is the CLASS String. This IS mutable
let mut b = String::from("hi")
```
String literals aren't mutable! if you want to change a string literal, you must make it into a ```String``` class either via ```String::from()``` or ```to_owned()```. You can also change ```Strings``` by passing its reference to a function:

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
let slice2: str = "wait this is a slice too?"
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

## String creation
there are multiple ways of creating ```Strings```.
```rust
let mut blank:String = String::new();
let s: String = String::from("From string literal");
let data = "initial contents";
let from_slice = data.to_string();
let direct = "directly from slice".to_string();
```

## ```push_str()``` and ```push()```
the prior appends a ```String``` whereas the latter appends a ```char```.
```rust
let s: String = String::from("hello ");
s.push_str("world");
s.push('!');
```
these methods **DOES NOT TAKE OWNERSHIP** of the passed strings.

## Concatenation Methods
there are two major ways of concatenation
### the + operator
```rust
//1. + operator
let s1 = String::from("Hello, ");
let s2 = String::from("world");
let s3 = s1 + &s2;
```
We can see from the last line that we actually pass a reference to String for the operator. Looking at the add function signature, the reason is clear:
```rust
fn add(self, &str) -> String {}
```
this means s2 will still be usable after concatenation!

### the ```format!``` macro
``` rust
let tic: String = String::from("tic");
let tac = "tac".to_string();
let toe: String = String::from("toe");
let ttt = format!("{tic}-{tac}-{toe}");
println!("{ttt}");
```
format macro works in the same way as the println macro, but it returns a String object instead of printing the thing out in stdout.

## Indexing and UTF-8 madness
in other languages, below is possible. Not in Rust. in Rust, String class is a Wrapper over a Vector of type u8. 
```rust
let s: String::from("Hello");
println!("throws error: {}", s[0]);
```
this is because Strings are encoded in UTF-8, and how letters are stored in each language differs. For example, a Russian letter takes up 2 8 byte blocks, Hindi takes 3 blocks, etc. Also, for some languages, the ```char``` values may not even be "letters". for example in Hindi letters can have diacritics, and each diacritic is considered to be its own character in UTF-8 encoding, but is not an actual letter by itself.

There are in total 3 ways of interpreting Strings
- Bytes
- Scalar Values
- Grapheme Clusters (most close to letters in NL)

Rust provides three ways of indexing/iterating characters
### range
```rust
let s: String = String::from("what is this madness");
let sl: &str = s[0..3]; //string slice uses range
```
while Rust does not let you use integer indexing, you can still use range. be careful, because as mentioned before, some languages can have multiple scalar values for one character. if your range stops within this range, the program will panic.
## char
```rust
let s: String = String::from("what is this madness");
for l in s.chars() {
	println!("{l}"); //will print characters as defined in UTF-8
}
```
## bytes
```rust
let s: String = String::from("what is this madness");
for l in s.bytes() {
	println!("{l}"); //will print binary value
}
```
this will print all binary value within the string

---
Categories: [[Rust]], [[Data Types]]
References: 
Created: 2024-05-09