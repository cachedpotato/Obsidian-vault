---
tags:
  - Rust
---
## What even are references?

Think of references as a pointer that points to a pointer that points to a heap. Simple!
you CAN use references for values stored in the stack, but more often than not you'll be using it for Strings and other values stored in heap. Take String for example:

```rust
fn main() {
  let s: String = String::from("hello");
  nom(s);
  //println!("{s}") <- won't work because it's used
}

fn nom(s: String) {
    println!("i ate {s}");
}
```

if a value is taken as a function argument, than **THE FUNCTION WILL TAKE OWNERSHIP**. Then how can you keep the original variable? With references, of course.

```rust
fn main() {
  let s:String = string::from("hello");
  nom_but_not_really(&s);
  println!("{s}")//this will work now
				  //because we passed the reference,
				  //not the actual variable
}

fn nom_but_not_really(s: &String) {
    println!("i ate the reference of {s}");
}
```

## Rules of References
There are also rules for references:
- One can have as many immutable reference as they want
- One can only have one mutable reference
- One must not have both mutable & immutable reference at the same time

What do we mean by "same time"? we refer to the scope of the reference, or should I say lifetime?
The scope of reference starts from the creation of said reference and ends at the line where it was last used. Knowing this, this is possible:
```rust
fn main() {
	let mut s: String = String::from("reference madness");
	let r1: &String = &s;
	let r2: &String = &s;
	//let r3: &mut String = &mut s; <- this is not possible
	ref_eat(r1, r2); //scope ends here
	let r3: &mut String = &s;
	println!("r3 works now: {r3}");
}
fn ref_eat(_r1: &String, _r2: &String) {
	//_r1 indicates I'm just passing the argument
	//but not actually using it
	println!("nom nom");
}
```


## References and printing
Normally, for languages like C/C++, if you try to print a pointer variable it will return the address:
``` C
int a = 3;
int* b = &a;
printf("{}", b); //gives address of b
```

However, in Rust, we don't get an address, but the value:
``` rust
let a: i32 = 3;
let b: &i32 = &a;
println!("{b}") //prints 3
```

to get the address of b, use the ```{:p}``` formatter:
``` rust
let a: i32 = 3;
let b: &i32 = &a;
println!("{:p}", b) //prints address of b
```
It's also worth noting that println! takes a reference of b, so regular mutation rules apply, meaning stuff like this is not possible:
``` rust
let a: i32 = 3;
let b: &mut i32 = &mut a;
println!("Imma print a: {a}"); //compile-time error
println!("This works tho: {b}"); //3
```
The first ```println!``` does not work because we're trying to pass a new immutable reference of a, when b, a mutable reference, already exist. However, because of how printing works in Rust, we can simply print b to print the value of a.
## Dangling Reference
A dangling reference is a reference that points to a blank space in heap. This can lead to memory safety issues. Make sure you don't have a dangling reference, though the compiler won't even compile if you have one.
```rust
fn dangler() -> &String {
	let s: String = String::from("Damn we danglin' now");
	
	&s //passing dangling reference as the output
}
```

## Reference related errors
Because of Rust's unique borrow checker, references can be hard to get used to. Here are some errors related to References that might be confusing at first.
- [[Rust Error E0716]]: Temporary value dropped while borrowed
- [[Rust Error E0506]]: Cannot assign to x because it is borrowed

---
Categories: [[Rust]] 
References:
Created: 2024-05-10