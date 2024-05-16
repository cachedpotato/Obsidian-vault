---
tags:
  - Rust
---
# Use
```use``` is a useful keyword to reduce repetition when calling modules/module functions.

Note that use will _ONLY APPLY ON THE SCOPE IT'S BEEN DECLARED_. 
```rust
mod front_of_house{
	pub mod hosting {
		pub fn add_to_waitlist() {}
	}
}

use crate::front_of_house::hosting;
//this_works is in the scope of use
pub fn this_works() {
	hosting::add_to_waitlist();
}

//we are now going inside the mod scope
//we won't be able to use the hosting shorthand 
mod back_of_house { 
	pub fn this_function_wont_work() {
		hosting::add_to_waitlist(); //this throws error
	}
}
```

## Creating idiomatic use Paths
even if it's tempting to just ```use``` the shortest shorthand possible for functions that will be used a lot of the time, the consensus is to import the parent module:
```rust
use crate::front_of_house::hosting::add_to_waitlist;
fn this_is_shorter() {
	add_to_waitlist();
}
```

```rust
use crate::front_of_house::hosting;
fn this_is_better() {
	hosting::add_to_waitlist();
}
```

for structs and enums, however, we use the whole path:
```rust
use std::collections::Hashmap; //Hashmap enum

fn main() {
	let mut map = Hashmap::new();
}
```

The exception to this rule is when two imported modules have identically named function:
```rust
use std::fmt;
use std::io;

fn function1() -> fmt::Result {}
fn function2() -> io::Result<()> {} //same name but different
//in cases like this, 
```

## the as keyword
to avoid confusion like the case above, we can use the ```as``` keyword to create an 'alias':
```rust
use std::fmt::Result as fResult;
use std::io::Result as iResult;

fn function1() -> fResult {}
fn function2() -> iResult<()> {}
```

## idiomatic use paths summary
- for enums/structs, use the full path
- for everything else, use the parent module
- if two modules share the same name, use as to create alias

## Re-exporting with pub use

^494caa

to bring an item into scope and also make that item available for others, we can use ```pub use```.
```rust
mod front_of_house {
	pub mod hosting {
		pub fn add_to_waitlist() {}
	}
}

pub use crate::front_of_house::hosting;
pub fn eat_at_restaurant() {
	hosting::add_to_waitlist();
}
```

## nested use paths
sometimes, we need to import a lot of modules.
if said module is big, then we may only use parts of it.
writing each use case one by one is tedious.
in this case, we can make nested use paths:
```rust
use std::cmp::ordering;
use std::io;
use std::io::Write;
```

```rust
use std::{cmp::ordering, io, io::Write};
```

```rust
use std::io::{self, Write} //imports std::io
						   // and std::io::write
```

use the ```self``` keyword if within the nested path, one module is the common denominator.

## glob operator
glob operator * works similar to the glob operator in bash:
```rust
use std::collections::*
```
above example will bring ALL public items into current scope.
## References

categories: [[Rust]]
Created: 2024-05-11