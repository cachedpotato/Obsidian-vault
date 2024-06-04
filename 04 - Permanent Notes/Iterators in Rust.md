---
tags:
  - NeedWork
---
# Iterators in Rust
The iterator is responsible for the logic of iterating over each item and determining when the sequence is finished.

``` rust
//loops
let mut i = 0;
let vec: Vector<i32> = vec![1, 2, 3];
while i < vec.len() {
	func(i);
}

//iterators
for item in vec.iter() {
	func2(item);
}
```
because iterator knows when to stop we don't need to specify the length of the vector as is the case with the while loop above. Using iterators can reduce errors stemming from manually setting when the loop should end.

## The Iterator [[Traits in Rust|trait]]
All iterators implement the ```Iterator``` trait that looks like this:
``` rust
pub trait Iterator {
	type Item;
	fn next(&mut self) -> Option<Self::Item>;
}
```
the ```type``` you see within the trait block is called an _associated type_. This means implementing the Iterator trait also requires you to define an Item type. 

You can make iterators as long as you implement the Iterator trait, which requires you to just 1) define the Item type and 2) implement the ```next``` function. Note that the function returns an Item wrapped in Option, to take care of end cases, where next should return nothing.

``` rust
let vec: Vec<i32> = vec![1, 2, 3];
let mut iter_vec = vec.iter();
println!("{:?}", iter_vec.next()); //Some(1)
println!("{:?}", iter_vec.next()); //Some(2)
println!("{:?}", iter_vec.next()); //Some(3)
println!("{:?}", iter_vec.next()); //None
```
**ITERATORS MUST BE MUTABLE FOR THEM TO CALL THE NEXT METHOD**.

## Iterator Methods
`iter_mut()` returns a _REFERENCE_, so you need to dereference it first to access and change value


## Methods that consume iterator
Methods that call ```next``` are called _consuming adaptors_, because it consumes the iterator. This means after calling the method the iterator is not reachable.
``` rust
let vec: Vec<i32> = vec![1, 2, 3];
let vec_iter = vec.iter();
let vec_sum = vec_iter.sum(); //iterator consumed here
println!("the sum of vector: {:?} is {}", vec, vec_sun);
println!("the iterator is already used", vec_iter); //does not work
```
the ```next()``` method also consumes the iterator.

## Methods that produce iterators
_iterator adaptors_ are methods defined on the Iterator trait that don't consume the iterator, and instead produce different iterators.
One extremely good example of this is ```map```.
``` rust
let vec: Vec<i32> = vec![1, 2, 3];
let vec_iter = vec.iter();
let vec_map = vec_iter.map(|x| x + 1); //just this does nothing
println!("{:?}", vec_map); //returns the OG iterator (no difference.)
```
Map is a method that takes [[Closure]] with [[Fn Traits#^148f86|FnMut]] trait. One important thing is that iterator adaptors are _lazy_ and will load only when its called.
``` rust
for item in vec_map {
	println!("now we loading. {:?}", item);
}

//we can also call collect
let v2: Vec<_> = vec.iter().map(|x| x + 1).collect();
assert_eq!(vec![2, 3, 4], v2);
```

``` filter``` method is also a iterator adaptor.
``` rust
struct Shoe {
	size: u32,
	style: String,
}
fn shoes_in_size(shoes: Vec<Shoe>, shoe_size: u32) -> Vec<Shoe> {
	shoes.into_iter().filter(|s| s.size == shoe_size)
}
```

## `iter()` vs `into_iter()`
there are two main methods of creating iterators: `iter()` and `into_iter()`. These two have a lot in common, with one key difference - ownership. `iter()` creates an `Iter` type that will iterate over the _borrowed_ values of the original collection, whereas `into_iter()` will essentially _transform_ the collection into an `IntoIter` object. Take joining threads using `map` for an example:
```rust
fn main() {
	//--snip
	let results: Vec<i32> = handles.iter()
		.map(|r| r.join().unwrap())
		.collect();
}
```
This will _NOT_ work because the ownership is moved when `join()` is called, but `r` itself is behind a shared reference. However, using `into_iter()` will work, since we have full ownership:
``` rust
fn main() {
	let results: Vec<i32> = handles.into_iter()
		.map(|r| r.join().unwrap())
		.collect();
}
```

## Functional Programming with Iterators

### Map

### Flatmap

### Filter
### Fold vs Reduce
1) Fold
```rust
let v: Vec<usize> = vec![0, 1, 2, 3, 4];
let sum: usize = v.fold(0, |acc, x| acc + x);
assert_eq(sum, 10);
```
`fold()` lets us explicitly type what our base case would be, and returns the raw summed/folded value.
2) Reduce
``` rust
let v: Vec<usize> = vec![0, 1, 2, 3, 4];
let sum = v.reduce(|acc, x| acc + x);
assert_eq(sum, Some(10));
```
`reduce()` implicitly creates the base case using the first element of the iterator, and returns the value wrapped inside an `Option<T>`.


## loops vs iterators
The age-old question: which is better?
loop is:
- Slightly slower
- Is NOT functional
- Easier to understand/debug

iterator is:
- slightly faster
- FUNCTIONAL BOIS (NO LOOPS! hopefully)
- Harder to get used to/debug

they all have their own strengths and weaknesses, but if you're going for a more functional approach, it's best to use iterators. so instead of for and while, use stuff like:

``` rust
a.iter() //iterator
	.map(|x| ...) //mapping (iterator adaptor)
	.filter(|&x, &y|...) //filtering
	.map()...
	.filter()...
	.collect() //consuming adaptor (add())
```



---
Categories: [[Rust]]
References:
Created: 2024-05-15
