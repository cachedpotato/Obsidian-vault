---
tags:
---
# The Deref Trait
Implementing the ```deref``` trait allows you to customize the behavior of the _deference operator_ ```*```. You can implement this trait to smart pointers in such a way that you can write code that operates on both references and smart pointers.

## How dereferencing works
Pointers are literally "pointers" that point to a value stored somewhere else. To access the value itself using the pointer, you need to _dereference_ it first.
``` rust
let x: i32 = 3;
let y = &x;

assert_eq!(3, x);
assert_eq!(3, *y);
assert_eq!(3, y); //this won't work - i32 and &i32 are DIFFERENT TYPES!
```
To mutate a value referenced by a pointer:
``` rust
let mut x:i32 = 3;
let y = &x;
*y += 1;
println!("x is now {y}"); //prints 4 
```

## Dereferencing Boxes
Box, being a smart pointer, has the ```Deref``` trait, and can be used similarly to a reference.
``` rust
fn main() {
	let x = 5;
	let y = Box::new(x); //5 stored in heap

	assert_eq!(x, 5);
	assert_eq!(*y, 5);
}
```
Difference here is that y is a [[Box]] that points to a value in heap that is a _COPY_ of x. Remember, integers like x have the copy trait, and reside in the stack.

## Making our own smart pointer
To create a smart pointer, we need the struct to implement the ```Deref``` trait.
``` rust
use std::ops::Deref;

struct MyBox<T>(T);

impl<T> MyBox<T> {
	fn new(x: T) -> Self {
		Self(x)
	}
}

impl<T> Deref for MyBox<T> {
	type Target = T;

	fn deref(&self) -> &Self::Target {
		&self.0
	}
}

fn main() {
	let y = MyBox::new(3);
	assert_eq!(*y, 3);
}
```
The ```type Target = T``` defines an [[Associated Types|associated type]] for the trait to use, Similar to how we have to define a type ```Item``` to implement the Iterator trait.

Notice how the ```deref``` function returns a reference, but dereferencing itself should not return a reference. This is because under the hood Rust does this:
```
*(y.deref())
```
when we do ```*y```. Rust does it like this because if we don't return a reference, the function will take ownership of the value, which is not what we want.

## Deref Coercion
Deref Coercion converts a reference to type that implements the ```Deref``` trait to a reference of another type. One of the best examples of this is ```String```. We've seen countless times throughout the book where we pass a ```&String``` to a function parameter that takes the type ```&str```.
``` rust
fn hello(name: &str) {
	println!("hello {name}!")
}

fn main {
	let s: Box<String> = Box::new(String::from("john"));
	hello(&s); //&Box<String> -> &str coercion
	hello("john"); //&str directly
}
```
Both uses of the ```hello``` function will result in the same output.
Deref coercion exists for convenience issues. If it didn't exist, we would have to write like the following:
``` rust
fn hello(name: &str) {
	println!("hello {name}!")
}

fn main {
	let s: Box<String> = Box::new(String::from("john"));
	hello(&(*s)[..]); 
	hello("john"); //&str directly
}
```
- ```*s```: responsible for Box(String) to String
- ```&(*s)```: responsible for String to &String
- ```&(*s)[..]```: responsible for &String to &str

When the ```Deref``` trait is defined for the types involved, Rust will analyze types and use ```Deref::deref``` as many times as it needs to match the signature of the reference it's trying to coerce to. Because all of this is done in compile time, there will be no runtime penalty!

## DerefMut and coercion of mutable references
Just like how you use ```Deref``` trait for * operator on immutable references, you can use the ```DerefMut``` trait for * operator on mutable references.

Rust does deref coercion when it finds types and trait implementation in three cases:

- From &T to &U when T: Deref<Target = U>
- From &mut T to &mut U when T: DerefMut<Target = U>
- From &mut T to &U when T: Deref<Target = U>

We can see coercion also works on mutable reference to immutable reference. However, the _**REVERSE IS NOT POSSIBLE**_. 










---
Categories: [[Traits in Rust]], [[Smart Pointer]]
References:
Created: 2024-05-17
