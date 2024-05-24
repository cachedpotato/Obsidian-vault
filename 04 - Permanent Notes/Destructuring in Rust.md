---
tags:
---
# Destructuring in Rust
We can use patterns to destructure structs, enums and tuples, with a combination of syntax used above.
### struct
``` rust
struct Point {
	x: i32,
	y: i32,
}

fn main() {
	let p: Point = Point {
		x: 3,
		y: 0,
	}

	let Point {x, y} = p;
	assert_eq!(x, 3);
	assert_eq!(y, 9);

	match p {
		Point{ x, y: 0 } => println!("at x axis with value {}", x),
		Point{ x: 0, y } => println!("at y axis with value {}", y),
		Point{ x: 1..=5, y: 3 | 4} => println!("custom pattern"),
		_ => println!("default"),
	}
}
```
In match we need to use the inclusive pattern `..=` for range and not `..` because that's used for something else.
Also note that if we pass range or multiple patterns, we can't just call the pattern like we normally do. For example,
``` rust
Point {x: 1..=6, y: 3 | 4} => println!("{}, {}", x, y)
```
will not compile. to print the exact value, we need something called the `@` binding.

### Enums
pattern matching Enum variants can be used in tandem with destructuring tuples, etc.
``` rust
enum Message {
	Quit,
	Write(String),
	Color(i32, i32, i32),
}

fn main() {
	let m1: Message = Message::Write(String::from("test"));
	let c1: Message = Message::Color(1,2,2);

	match m1 {
		Message::Quit => println!("Quit"),
		Message::Write(s) => println!("{s}"),
		_ => println!("Default"),
	}
	match c1 {
		Message::Color(r, g, b) => {
			println!("r: {r}, g: {}, b: {}", g, b);
		},
		_ => (),
	}
}
```

we can mix and match destructuring patterns however we please, meaning this is possible
``` rust
let ((feet, inches), Point {x, y}) = ((3, 10), Point{x: 1, y: 10});
```

---
Categories: [[Pattern Syntax in Rust]]
References:
Created: 2024-05-24
