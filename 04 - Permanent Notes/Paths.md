---
tags:
  - Rust
---
# Paths
a path can take two forms, just like in filesystem:
- Absolute path: start from crate root (crate)
- Relative path: start from current module
	- use self, super

## what goes in the lib.rs file?
^945cfc
lib.rs is the root if library crate. while main.rs in binary crate is the home of fn main() function, library crates don't have that. instead, they define the module tree:
```rust
//lib.rs
//define module tree (If we were to make it all in one file)
mod front_of_house {
	pub mod hosting {
		fn add_to_waitlist() {}
		pub fn seat_at_table() {}
	}
	mod serving {
		fn take_order() {}
		fn serve_order() {}
		fn take_payment() {}
	}
}
```

## pub and private
even if you have the path set up, whether other function will be able to use the modules is decided by privacy state. if it's public, then other modules can use them. If not, compiler will throw an error.
## self and super
for relative paths, Rust use the ```self and super``` keys.
- ./... : self:: ...
- ../...: super:: ...
```rust
fn deliver_order() {} //at a higher level

mod back_of_house {
	fn fix_incorrect_order() {
		cook_order();
		super::deliver_order(); //using function a level higher
								//than back_of_house module
	}
}

//tree wise:
// /deliver_order()
// /back_of_house/fix_incorrect_order() <- one level below
```
the self key is hidden - you don't need to write it yourself.

## separating modules into different files
if things get large we may want to split into little pieces for better organization. using the restaurant module mentioned [[Paths#^945cfc|above]], we can split as the following:

- lib.rs
```rust
mod front_of_house;
```
Notice that we removed the brackets.
To move submodules/functions to a new file, in the parent file add a mod declaration in the style of ```mod modname;```.

- front_of_house.rs
```rust
pub mod hosting;
mod serving;
```

- front_of_house/hosting.rs
```rust
fn add_to_waitlist() {
	//--snip
}

pub fn seat_at_table() {
	//--snip
}
```
- front_of_house/serving.rs
```rust
fn take_order() {
	//--snip
}
fn serve_order() {
	//--snip
}
fn take_payment() {
	//--snip
}
```

## References

categories: [[011-Rust]]
Created: 2024-05-11