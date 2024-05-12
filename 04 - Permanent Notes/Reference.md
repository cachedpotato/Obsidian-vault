---
tags:
  - Rust
---
## What even are references?

Think of references as a pointer that points to a pointer that points to a heap. Simple!
you CAN use references for values stored in the stack, but more often than not you'll be using it for Strings and other values stored in heap. Take String for example:

```rust
fn main() {
  let s:string = string::from("hello");
  nom(s);
  //println!("{s}") <- won't work because it's used
}

fn nom(s: string) {
    println!("i ate {s}");
}
```

if a value is taken as a function argument, than **THE FUNCTION WILL TAKE OWNERSHIP**. Then how can you keep the original variable? With references, of course.

```rust
fn main() {
  let s:String = string::from("hello");
  nom_but_not_really(&s);
  println!("{s}") //this will work now
				  //because we passed the reference,
				  //not the actual variable
}

fn nom_but_not_really(s: &String) {
    println!("i ate the reference of {s}");
}
```

There are also rules for references
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

## Dangling Reference
A dangling reference is a reference that points to a blank space in heap. This can lead to memory safety issues. Make sure you don't have a dangling reference, though the compiler won't even compile if you have one.
```rust
fn dangler() -> &String {
	let s: String = String::from("Damn we danglin' now");
	
	&s //passing dangling reference as the output
}
```

---
Categories: [[Rust]] 
References:
Created: 2024-05-10