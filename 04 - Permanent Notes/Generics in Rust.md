---
tags:
  - Rust
---
# Generics in Rust
It's always good practice to abstract out repeated code into a single function. What if we have functions that does the same time, but with different types?
```rust
fn largest_i32(list: &[i32]) -> &i32 {
	let largest = &list[0];
	for i in list {
		if i > largest {i = largest;}
	} 
	largest
}
fn largest_char(list: &[char]) -> &char {
	let largest = &list[0];
	for i in list {
		if i > largest {i = largest;}
	} 
	largest
}
fn largest_float(list: &[f32]) -> &f32 {...}
```

This seems highly repetitive and frankly is a waste of time and code. How do we fix this? we can use generics to account for all types!

```rust
fn largest <T> (list: &[T]) -> &T {
	let largest = &list[0];
	for i in list {
		if i > largest {i = largest;}
	} 
	largest
}
```

the ```<T>``` at the right side of the function name indicates the generic type. In this case whenever a generic type must be used we need to annotate it using T. 

_HOLD UP_ - this won't compile. That's because of the comparison operator '>'. Because we're using generics, we need to make sure whatever's passed into this function can be compared by size. In other words, the generics must have a certain **trait** that allows us to compare.

```rust
fn largest <T: std::cmp::PartialOrd> (list: &[T]) -> &T {
	...
}
```

## Generics for struct and enum
we can also use generics for struct and enum, like so:
```rust
struct Point <T> {
	x: T,
	y: T,
}

enum Option<T> {
	Some(T),
	None
}
```
Yes, its _THAT_ Option enum that we've seen countless times

## Multiple generics
Say we want to make a struct called Point with generics.
```rust
struct Point <T> {
	x: T,
	y: T,
}

fn main() {
	let p = Point{
		x: 1, //i32
		y: 0.5 //float
	}
}
```

This won't compile, because we only used ONE generic type T. because x and y are of different types, This cannot be compiled. What do we do? Just add more generics!

```rust
struct Point<X1, Y1> {
	x: X1,
	y: Y1,
}

fn main() {
	let p = Point{
		x: 1, //i32
		y: 0.5 //float
	}
}
```

## Methods with generic types
What do we do if we want to [[Implementation|implement]] methods for our struct?
```rust
impl <X1, Y1> Point <X1, Y1> {
	fn get_x_ref(&self) -> &X1 {
		&self.x
	}
}
```
Notice how we declare generics two times, first for impl and the latter for Point. Think of the entirety of ```Point<X1, Y1>``` as the name of the struct. From this point of view, we are simply letting impl know we are using generics of the names X1 and Y1, just like how we did for struct Point.

What if we want to implement methods for specific types? say for struct Point, we might want to get Euclidian distance for float.

```rust
impl Point<f32, f32> {
	fn distance_from_origin(&self) -> f32 {
		(self.x.powi(2) + self.y.powi(2)).sqrt()
	}
}
```

See how we did not have to add ```<f32>``` next to impl. This is because from the implementation's POV, we aren't using generics. However, we still need to specify what type we're using for the struct, hence the ```Point<f32, f32>```.

We can add as many generic types as we wish, like so:
```rust
impl <X1, Y1> Point<X1, Y1> {
	fn swap <X2, Y2> (self, other: Point<X2, Y2>) -> Point<X1, Y2> {
		Point {
			x: self.x,
			y: other.y
		}
	}
}
```

On a side note - since we are 1. passing ```self``` and not ```&self``` and 2. we are passing ```Point<>``` and not ```&Point```, _BOTH_ variables used for this swapping process will be gone. Ownership am I rite?



---
Categories: [[011-Rust]], [[Data Types]]
References:
Created: 2024-05-14
