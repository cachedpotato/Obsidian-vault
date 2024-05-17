---
tags:
---
# Rc
Most of the time there is only one owner for a given value. However, there are cases where we might want to have multiple owners. Consider graphs for example. A node may be connected to multiple edges, which conceptually acts as the owner of the node.

With regular references, this concept of graphs is not possible. This is where Reference counter, abbreviated to ```Rc```, comes in play.

```Rc<T>``` keeps track of the number of references to a value to determine if the value is still in use. if the count reaches zero, it will promptly be cleaned up without leaving room for dangling references.

## When do we use Rc?
```Rc<T>``` is used when we want to allocate data on the heap for _multiple parts of our program to read_ and we _can't determine which program will finish last during compile time._ If we did know, then there's no need for Rc, as we can just make that part the data's owner. In other words, we use Rc when we want to share data and we're unsure how each program that shares the data will process their own thing and terminate.

It's also important to know ```Rc<T>``` is only for **Single treaded scenarios**. There are different measures to take for multithreaded programs.

## An example case of Rc
Consider two lists that both share ownership of a third list.
![[trpl15-03.svg]]
Let's use Cons and Box first to turn this concept into code.
``` rust
enum List {
	Cons(i32, Box<List>),
	Nil,
}
use List::{Cons, Nil};
fn main() {
	let a: List = Cons(5, Box::new(Cons(10, Box::new(Cons(Nil)))));
	let b: List = Cons(3, Box::new(a));
	let c: List = Cons(4, Box::new(a));
}
```
This won't compile, because a has already been moved to b, but c is trying to access a.

One quick solution that might come to mind is using references. However, now we need to specify Lifetimes (see [[Rust Error E0716]] for more info on why we do this madness):
``` rust
enum List<'a> {
	Cons(i32, Box<&'a List<'a>>),
	Nil,
}
use List::{Cons, Nil};
fn main() {
	let nil: List = Nil;
	let l10: List = Cons(10, Box::new(&nil));
	let a: List = Cons(5, Box::new(&l10));
	let b: List = Cons(3, Box::new(&a));
	let c: List = Cons(4, Box::new(&a));
}
```
This is DEFINITELY NOT WHAT WE WANT. This also assumes that the elements within the List will live at least as long as the List itself, which is not always the case.

To avoid this madness, we will use ```Rc<T>``` instead of ```Box<T>```.
``` rust
use std::rc::Rc;
enum List {
	Cons(i32, Rc<List>),
	Nil,
}

use List::{Nil, Cons}
fn main() {
	let a: List = Rc::new(Cons(5, Rc::new(Cons(10, Rc::new(Nil)))));
	let b: List = Cons(3, Rc::clone(&a));
	let c: List = Cons(4, Rc::clone(&a));
}
```
Make sure to wrap the value you want to share with ```Rc``` as well, like the ```a``` above.
Wait. CLONING??? NOT IN MY HOUSE - chill, hold your horses. This is not a _deep clone_ where you clone everything, this is just a clone of the reference. That is not to say cloning is impossible, it's just highly inefficient.
## Cloning and Reference Count
As stated above, ```Rc``` keeps track of reference counts, and whenever we do a ```Rc::clone()```, we increase the count by 1. We can get the amount of references by using ```strong_count()```:
``` rust
let a = Rc::new(Cons(5, Rc::new(10, Rc::new(Nil))));
println!("count after creating a = {}", Rc::strong_count(&a));
let b = Rc::new(Cons(3, Rc::clone(&a));
println!("count after creating b = {}", Rc::strong_count(&a));
{
	let c = Rc::new(Cons(4, Rc::clone(&a));
	println!("count after creating c = {}", Rc::strong_count(&a));
}
println!("count after c goes out of scope: {}", Rc::strong_count(&a));
```
Result:
```
cargo run
count after creating a = 1
count after creating b = 2
count after creating c = 3
count after c goes out of scope: 2
```

---
Categories: [[Smart Pointer]]
References:
Created: 2024-05-17
