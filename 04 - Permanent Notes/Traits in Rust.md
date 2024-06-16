---
tags:
  - Rust
---
# Traits in Rust
A trait defines a functionality a given type has and can share with other types. We can also use traits as boundaries for [[Generics in Rust|generics]] as seen before with the ```PartialOrd``` trait.

## Defining a trait
Just like how we define methods, we can define traits with the ```trait``` keyword. In essence, a trait is a collection of methods we can call on that type. 

Think of a hypothetical situation where we're handling tweets and newspaper articles. While they're not COMPLETELY identical, they can still share similar traits. Maybe we can both _summarize_ its content. Why don't we add a trait for that?
```rust
pub trait Summary {
	fn summarize(&self) -> String;
}
```

Notice how we only _declared_ the function, and not have the actual content of the function in it. this is because how function works will differ from type to type. Of course, if all types with this trait implements the ```summarize``` function identically, then we can add the content within this block, just like impl:

```rust
pub trait Summary {
	fn summarize(&self) -> String {
		//your code goes here..
	}

	fn another_characteristics(&self) -> usize;
	//...
}
```

This is called the **Default Implementation**, and if there does not exist type specific implementation for a given trait, it whatever function within this trait is called, it will use this.
## Implementing a trait
Now that we've declared a trait, how do we actually use it? Going back to the tweet/newspaper example, how do we implement the Summary trait for struct tweet?

```rust
pub struct Tweet {
	pub length: u8, //doesn't exceed 200 words - cut dat memory usage
	pub author: String,
	pub likes: usize,
	pub text: String,
}

impl Summary for Tweet {
	fn summarize(&self) -> String {
		let mut summary: String = String::new();
		//something related to self.text I assume

		sumnmary
	}
}

pub struct NewsPaper {
	pub length: usize,
	pub author: String,
	pub press: String
	pub text: String
}

impl Summary for NewsPaper {
	fn summarize(&self) -> String {
		let mut summary: String = String::new();
		//something related to self.text
		//but probably different from Tweet struct

		summary
	}
}
```
basically, we use ```impl [trait name] for [type]```. 

## Orphan Rule

^240317

So far we've seen how we can implement traits defined within our crate to types also defined in our crate. What if we want to implement our own traits to types defined outside of our crate, say, `Summary` on `Vec<T>`, or the other way around, let's say an external trait like `std::fmt::Display` to our custom type `NewsPaper`? Is it even possible?
Why, yes it is!
```
impl<T> Summary for Vec<T> {
	fn summarize(&self) -> String {...}
}

impl std::fmt::Display for NewsPaper {
	fn fmt(&self, f: fmt::Formatter) {...}
}
```
However, we **CANNOT** implement `Display` on `Vec<T>` in our crate, because they are both not defined here. This is the orphan rule of traits. In summary:

- _we can implement traits on a type if and only if at least one of the trait or type is local to the crate_

## Trait as parameters
besides using trait as a "characteristic" of a type, we can also pass it as a parameter. There are two kinds of ways it's used

### for function argument
```rust
pub fn notify(item: &impl Summary) {
	println!("New article: {}", item.summarize())
}
```

instead of notating types such as usize, i32, etc., by using the trait as the parameter, this function can take _ANY TYPE_ that has the Summary trait. Note that the above is a shrunken down version of this:

### Trait bound syntax
```rust
pub fn notify <T: Summary>(item: &T) {...}
```
...Hey, we've seen this [[Generics in Rust|before]]! To use the shortened version or the "standard" version is up to you, but if things get too complicated, it's best to use the latter. 

## Multiple trait bounds
sometimes, just one trait isn't enough. To add multiple trait bounds, do it like so:
```rust
pub fn multiple_traits(item: &(impl Trait1 + Trait2)) {...}
//Do this cooler version instead
pub fn multiple_traits <T: Trait1 + Trait2> (item: &T) {...}
```

## ```where``` clause
Look at this mess:
```rust
fn convoluted_funciton <T: Trait1 + Trait2, U: Trait3 + Trait4> (item: &T, item2: &U) -> usize {...}
```
...Yikes. If things get too long, we can make it look more concise with the ```where``` clause, like so:

```rust
fn convoluted_function <T, U> (item: &T, item2: &U) -> usize
where
	T: Trait1 + Trait2
	U: Trait3 + Trait4
{...}
```

## Traits for output
we can also use trait bounds for output:
```rust
fn trait_bound_output(x: i32, y: String) -> impl Summary {...}
```
However, this **DOES NOT MEAN YOU CAN RETURN MULTIPLE TYPES**. In other words, we can't make this function return either a ```NewsPaper``` or a ```Tweet```. 

## Conditional Implementation of Methods
Just like how we add trait boundaries for functions to use only a given subset of generics, we can do the same with implementation. In other words, we can _conditionally implement_ methods.

```rust
use std::fmt::Display;

struct Pair<T> {
	x: T,
	y: T,
}

impl <T> Pair<T> {
	fn new(x: T, y: T) -> Self { //Self the type not self the instance
		Self {
			x,
			y,
		}
	}
}

impl <T: Display + PartialOrd>  Pair<T> {
	fn cmp_display<&self> {
		if self.x >= self.y {
			println!("the bigger value is x: {}". self.x);
		}
		else {println!("the bigger value is y: {}"), self.y};
	}
}
```

_**WHEW**_. That was a LOT to unpack. Goes to show how intricate generics can get.

---
Categories: [[011-Rust]]
References:
Created: 2024-05-14
