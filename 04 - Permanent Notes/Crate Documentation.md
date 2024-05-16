---
tags:
---
# Crate Documentation
Documentation comments use three slashes instead of two, and supports **MARKDOWN NOTATION**.
``` rust
/// Adds one to the number given.
///
/// #Examples
/// ```
/// let arg: i32 = 5;
/// let answer = my_crate::add_one(arg);
/// assert_eq!(6, answer);
/// ```
///
pub fn add_one(x: i32) -> i32 {
	x + 1
}
```
run ```cargo doc --open``` to see the actual HTML page. The example above will look like the following:
![[trpl14-01.png|500]]
Note that the Example block _HAS ITS OWN SCOPE_, meaning even if it's defined within the main lib.rs, it will act like it doesn't know where anything is. When writing examples block, write it like _you're the user not the developer_. From a developer's perspective everything is in scope, but for the normal user they need to explicitly bring modules in to use it.

## Commonly used sections
Besides Examples, there are other sections that are commonly used.
1) Panics
``` rust
/// Panics for the sake of panicking.
///
/// #Panics
/// ```
/// panic!("AAAAAAAAAAAAAAAAA");
/// ```
```

2) Errors
if a function returns a result, describing the kinds of errors that might occur can be helpful.
``` rust
/// Attempts to unwrap option. returns Err(str) if failed.
/// #Errors
/// ```
/// let x: Option<i32> = None;
/// if let Err(s) = unwrapper(x) {
///   println!("{s}");
/// }
fn unwrapper <T> (x: Option<T>) -> Result<T, &'static str> {
	match x {
		Some(o) => {return Ok(o)},
		None => {return Err("failed to unwrap")}
	}
}
```

3) Safety
If the function is ```unsafe```, there should be a section explaining why it's unsafe.

## Documentation Comments as tests
When ```cargo test``` is run, and you also have Documentation Comments with code snippets, it will also run those as well. This means by making docs you're essentially making test cases as well!

```
Doc-tests rust_crates

running 1 test
test src/lib.rs - add_one (line 5) ... ok

test result: ok. 1 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out; finished in 0.13s
```
the results will look something like the above.

## Commenting Contained Items
```//!``` adds documentation to the item that contains the comments We typically use these comments inside the crate root file or inside a module to explain the big picture.
``` rust
//! #My crate
//!
//! `my_crate` is a collection of utilites blah blah blah

/// Adds one to the number given
/// #Examples
/// ....
fn add_one(x:i32) -> i32 { x + 1 }  
```



---
Categories: [[Crates.io]]
References:
Created: 2024-05-16
