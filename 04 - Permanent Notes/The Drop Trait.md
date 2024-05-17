---
tags:
---
# The Drop Trait
If the ```Deref``` trait managed the Smart pointer's ways of handing the dereference operator * , the ```Drop``` trait lets you customize what happens when a value is about to go out of scope. Both ```Deref``` and ```Drop``` traits are an essential part of smart pointers.

This trait is used almost solely in the context of small pointers, as variables in the stack don't need manual freeing of memory. One thing about ```Drop``` trait that's different than the likes of ```drop()``` in other low-level languages is that it's highly customizable and once your smart pointer implements it, you don't need to call it manually!

The Drop trait is included in the prelude.
``` rust
struct CustomPointer {
	data: String,
}
impl Drop for CustomPointer {
	fn drop(&self) {
		println!("Custom Destructor Message");
	}
}

fn main() {
	let x: CustomPointer = CustomPointer {
		data: String::from("some data"),
	}
	println!("x has been created with data: {}", x.data);
}
```

The output of cargo run would look something like this:
```
cargo run
x has been crated with data: some data
Custom Destructor Message
```

## drop() method and destructor drop()
while we can create custom destructors by implementing this trait, this does not mean we can call them explicitly. Rust will raise a compile error if we try to do so, to prevent double free error. However, that is not to say we can't destruct something during runtime. I know it's confusing, but we can use the drop _function_ for this:

``` rust
use std::mem::drop;
//--snip
fn main() {
	let x: CustomPointer {
		data: String::from("some data"),
	} 
	prinln!("CustomPointer x created");
	x.drop(); //this is not possible
	drop(x) //but this is
	println!("exiting program...");
}
```
Results:
```
cargo run
CustomPointer x created
Custom Destructor Message
exiting program...
```


---
Categories: [[Traits in Rust]], [[Smart Pointer]]
References:
Created: 2024-05-17
