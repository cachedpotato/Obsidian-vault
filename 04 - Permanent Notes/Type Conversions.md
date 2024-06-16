---
tags:
---
# Type Conversions in Rust
there are many ways of converting one type to the other, and most of them are done by implementing certain traits. However, for quick conversions, we can use `as` for typecasting:
```rust
let a: usize = 30;
let b: usize = 24;
let c: f64 = a as f64 / b as f64;
```
Below are traits for conversions.
## From and Into
The `From` trait, when implemented, lets us create some variable of type `U` from a different type `T`. The `from()` and `into()` are kind of twins, where they essentially create the same value, but with slightly different routes:
```rust
let s: &str = "9";
let using_from = u8::from(s);
let using_into: Result<u8, _> = s.into();

assert_eq!(using_from, using_into.unwrap());
```
`from` is used as an associated function of the type we're trying to transform into, and returns the type itself. `into`, on the other hand, returns `Result<U, _>`, and the type must be explicitly written on the left hand side next to `:`.
## TryFrom & TryInto
`TryFrom` trait is a 'safer' version of `From`, where the `try_from()` returns a `Result<T>` instead of the raw type. Note that `TryFrom` has an associated type for error handling.
``` rust
use std::convert::{TryFrom, TryInto};

struct Color {
	red: u8,
	green: u8,
	blue: u8,
}

enum ColorError {
	ConversionError,
	OtherError,
}

impl TryFrom<(i16, i16, i16)> for Color {
	type Error = ColorError
	fn try_from(tuple: (i16, i16, i16)) -> Result<Self, Self::Error> {
		let red = u8::try_from(tuple.0)
			.map_err(|_| ColorError::ConversionError)?;
		let green = u8::try_from(tuple.1)
			.map_err(|_| ColorError::ConversionError)?;
		let blue = u8::try_from(tuple.2)
			.map_err(|_| ColorError::ConversionError)?;

		Ok(Color {
			red,
			green,
			blue,
		})
	}
}

fn main() {
	let c = Color::try_from((14, 240, 39)).unwrap();
	let ci: Color = (40, 123, 11).try_into().unwrap();
}


```

## `FromStr`
`FromStr` trait lets you create type instances from string literals with the `from_str()` and `parse::<U>` method!
```rust
use std::conversion::
#[derive(PartialEq, Debug)]
struct Point {
	x: usize,
	y: usize,
}
#[derive(Debug)]
struct PointConversionError;

impl FromStr for Point {
	type Err = PointConversionError
	fn from_str(s: &str) -> Result<Self, Self::Err> {
		let v = s.splice(',').collect::<Vec<&str>>();
		if v.len() != 2 {return PointConversionError}

		let x = v[0].parse::<usize>()
			.map_err(|_| PointConversionError)?;
		let y = v[1].parse::<usize>()
			.map_err(|_| PointConversionError)?;

		Ok(Point {
			x,
			y,
		})
	}
}

fn main() {
	let p = "10,20".parse::<Point>().unwrap();
	let p1: Point = Point::from_str("10,20");
	assert_eq!(p, p1);
}
```


---
Categories: [[011-Rust]], [[Traits in Rust]]
References:
Created: 2024-06-03
