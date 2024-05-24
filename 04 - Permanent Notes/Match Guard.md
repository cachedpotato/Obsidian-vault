---
tags:
---
# Match Guard
We can add another layer to pattern matching with match guards, which are additional `if` statements that are _NOT_ considered a pattern. 
``` rust
let x = Some(10);
match x {
	Some(n) if n%2 == 0 => println!("x is even number {}", x),
	Some(n) => println!("x is some number {}", x),
	_ => println!("x is None"),
}
```
doing cargo run results in `x is even number 10`.
We can also use match guards to get environmental variables.
``` rust
let x = Some(10);
let y = 5;
match x {
	Some(n) if n > y => println!("x is some number {n} bigger than {y}"),
	_ => pritnln!("default"),
}
```


---
Categories: [[Pattern Syntax in Rust]]
References:
Created: 2024-05-24
