---
tags:
---
# Ignoring Values in Pattern Matching
We can ignore values altogether with `_` as a prefix, or `..` to ignore remaining parts of a value.

### `_`

``` rust
let (a, _, b, _, c) = (1, 2, 3, 4, 5);
println!("{} {} {}", a, b, c);
```

### `..`

We can use the `..` pattern to ignore remaining fields of a struct, or parts of a tuple, etc.

``` rust
struct 3DPoint {
	x: i32,
	y: i32,
	z: i32,
}

fn main() {
	let p = 3DPoint {
		x: 0,
		y: 1,
		z: 2,
	}	
	match p {
		Point {x, ..} => println!("x is {}", x),
	}

	let t = (1, 2, 3, 4, 5);
	match t {
		(a, .., b, c) => {println!(
			"first: {}, second to last: {}, last: {}",
			a, b, c
		)}
	}
}
```
Note that `..` can only be used ONCE per tuple pattern to remove ambiguity. If we write something like `(.., second, ..)` the compiler doesn't know exactly what element `second` refers to.

---
Categories: [[Pattern Syntax in Rust]]
References:
Created: 2024-05-24
