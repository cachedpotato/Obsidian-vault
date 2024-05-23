---
tags:
---
# Fn Traits
```Fn``` [[Traits in Rust|traits]] are traits that are implemented by closures, and there are three types: ```FnOnce, FnMut, and Fn```. Closures can implement any of these traits in an additive fashion depending on how it handles environment values.

## ```FnOnce```

^34e9a7

This applies to closures that can be called once. _All closures implement this trait_. A closure that moves captured values out of its body will only implement ```FnOnce``` because it can only be called once.
``` rust
impl <T> Option<T> {
	pub fn unwrap_or_else(self, f:F) -> T
	where
		F: FnOnce() -> T
	{
		match self {
			Some(x) => x,
			None => f(),
		}
	}
}
```
Looking at the None case, we can see the closure takes nothing as input parameters, and outputs a generic type T. 

## ```FnMut```

^148f86

This is used when the closure _Mutates_ its environment. ```FnMut``` can also be called (more than) once meaning it has the definitions of ```FnOnce``` inside itself. This is what we mean by closures implementing in an _additive_ fashion.

``` rust
struct Rectangle {
	width: u32,
	height: u32,
}

fn main() {
	let mut list = [
		Rectangle { width: 10, height: 1 },
		Rectangle { width: 5, height: 3 },
		Rectangle { width: 9, height: 7 },
		Rectangle { width: 30, height: 14 },
	]

	list.sort_by_key(|r| r.width);
	println!("{:?}", list);
}
```

the ```sort_by_key()``` takes an argument (a Rectangle in this case) as a reference, and _MUTATES_ it into some value K (width in this case) that can be ordered. think of ```.as(fn => {})``` thingy from JS. This is why ```FnMut``` trait is implemented here.

## ```Fn```
This takes an immutable receiver, and instances of this can be called repeatedly without mutating state. This is implemented automatically by closures that only take immutable references to captured variables or just don't capture anything at all.

```FnOnce``` and ```FnMut``` are supertraits of this, so ```Fn``` can be used as a parameter where these two are needed.

``` rust
fn call_with_one<F> (func: F) -> usize
where
	F: Fn(usize) -> usize
{
	func(1)
}
let the_closure = |x| x*2
assert_eq!(call_with_one(the_closure), 2);
```





---
Categories: [[Rust]], [[Closure]]
References:
Created: 2024-05-15
