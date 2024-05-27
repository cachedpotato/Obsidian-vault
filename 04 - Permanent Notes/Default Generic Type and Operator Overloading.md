---
tags:
---
# Default Generic Type and Operator Overloading
When we use generic type parameters, unlike other parameters we can actually specify the default type, like so:
```rust
struct MyGenericType<T = DefaultType> {...}
```
This can be useful with operator overloading.

## Connection with Operator Overloading
Consider the case of a struct `Point`. We may want to add said Points to get a new vector, which can be done by implementing the `Add` trait:
``` rust
use std::ops::Add;

#[derive(Debug, PartialEq)]
struct Point {
	x: i32,
	y: i32,
}
impl Add for Point {
	type Output = Point;
	fn add(self, rhs: Point) -> Point {
		Point {
			x: self.x + rhs.x,
			y: self.y + rhs.y,
		}
	}
}

fn main() {
	assert_eq!(Point{x:0, y:2} + Point{x:1, y:2}, Point{x:1, y:4});
}
```
The need for the [[Associated Types|associated type]] for the implementation comes from the definition of the Add trait:
```rust
pub trait Add<Rhs=Self> {
	type Output;
	fn add(self, rhs:Rhs) -> Self::Output;
}
```
We can also see that in the definition the Default type for the generic type is used. This is why when we implemented `Add` for our `Point`, we didn't have to specify the type - the Default (`Point`) was automatically implemented.

This means that we can add two different types with the `+` operator!
``` rust
struct SimplifiedPoint(i32, i32);
impl Add<SimplifiedPoint> for Point {
	type Output = Point;
	fn add(self, other: SimplifiedPoint) -> Point {
		Point{
			x: self.x + rhs.0,
			y: self.y + rhs.1 
		}
	}
}

fn main() {
	assert_eq!(Point{x:1, y:1} + SimplifiedPoint(2, 3), Point{x: 3, y: 4});
}
```

To summarize, using default generic type and associated types can be useful when we're doing operator overloading, and the basic structure is like so:
```rust
pub trait OverLoading<T=DefaultType> {
	type Out;
	fn operator(&self, other:T) -> Self::Out {...}
}
```

---
Categories: [[Advanced Traits]]
References:
Created: 2024-05-27
