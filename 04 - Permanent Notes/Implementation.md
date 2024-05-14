---
tags: 
parent:
---
# Implementation
all functions within the implementation box is called associated function.
methods are associated function that has either ```self or &self``` as its fist argument. not that ```self or &self``` is a shorthand version of ```self: Self or self: &Self```, where Self means the type of the struct itself.

```rust
struct Rectangle {
	height: 30,
	width: 40,
}

impl Rectangle {
	fn area(&self) -> u32 {
		self.height * self.width
	}
}

//impl blocks can be seperated in any order
impl Rectangle {
	fn builder(height: u32, width: u32) -> Rectangle {
		Rectangle {
			height,
			width
		}
	}
}
```

---
Categories: [[Rust]]
Reference: 
Created: 2024-05-11