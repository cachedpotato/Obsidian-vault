---
tags:
---
# Associated Types
Associated types connect a type _placeholder_ with a trait such that the trait method definitions can use the placeholder types in their signatures. The implementor of said trait must specify the concrete type for the placeholder.

We've seen an example of associated types with [[Iterators in Rust|Iterator]] trait:
```rust
pub trait Iterator {
	type Item;

	fn next(&mut self) -> Option<Self::Item>;
}
```
The `Item` type is the placeholder for the output type of `next()` method, as can be seen in `Option<Self::Item>`. Say we want to implement this for our `Count` type.
``` rust
struct Count {
	c: u32,
}
impl Iterator for Count {
	type Item = u32;
	fn next(&mut self) -> Option<Self::Item> {
		match self.c {
			n@0..=10 => Some(n + 1),
			_ => None,
		}
	}
}
```
We have specified our `Item` to be `u32`.

## Associated types vs Generic types
Associated types acting as a placeholder sounds a lot like generic types. Why not use that then? What's stopping me from doing this?
``` rust
pub trait Iterator<T> {
	fn next(&mut self) -> Option<T>;
}
```
Let's try to implement Iterator this way.
``` rust
pub trait MyIterator<u32> {
	fn next(&mut self) -> Option<u32>;
}
impl MyIterator<u32> for Counter {
	fn next(&mut self) -> Option<u32> {...}
}
```
This may seem harmless at first, but making the trait this way means we can have _multiple implementations of Iterator trait_. We can have `MyIterator<String>`, `MyIterator<char>`, the list goes on. This also means that we may have to annotate which implementation of `MyIterator<T>` we're trying to use whenever we call `next()` method, which is quite cumbersome.
If we use associated types, there can _only be one implementation_, which gets rid of unnecessary annotations.

---
Categories: [[Advanced Traits]]
References:
Created: 2024-05-24
