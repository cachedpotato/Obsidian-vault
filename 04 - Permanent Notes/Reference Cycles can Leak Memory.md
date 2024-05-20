---
tags:
---
# Reference Cycles can Leak Memory
Rust is generally memory safe. That is not to say it is absolutely free from memory leak. In fact, with the "right" combination of smart pointers, we can not only create memory leak, we can cause the program to stack overflow!
``` rust
use std::rc::Rc;
use std::cell::RefCell;

#[derive(Debug)]
enum List {
	Cons(i32, RefCell<Rc<List>>),
	Nil,
}

impl List {
	fn tail(&self) -> Option<&RefCell<Rc<List>>> {
		match self {
			Cons(_, item) => Some(item)
		}
	}
}

use List::{Cons, Nil};
fn main() {
	let a = Rc::new(Cons(5, RefCell::new(Rc::new(Nil))));
	println!("tail of a: {:?}", a.tail()):
	
	let b = Rc::new(Cons(10, RefCell::new(Rc::clone(&a))));
	println!("b after creation: {:?}", b);

	//cycle creation
	if let Some(item) = a.tail() {
		*item.borrow_mut() = Rc::clone(&b);
	}

	println!("strong count of a: {}", Rc::strong_count(&a));
	println!("strong count of b: {}", Rc::strong_count(&b));

	//THIS IS WHERE IT GOES DOWN
	println!("tail of a: {:?}", a.tail());
}
```
the last strong count printing results to:
```
strong count of a: 2
strong count of b: 2
```
which seems normal. we created a and b and wrapped it with ```Rc```, so that's one, and because a is pointing to b and vice versa, we need to add one to the strong count, which results in 2.

Now let's try to print the last line:
```
...{ value: Cons(10, RefCell { value: Cons(5, RefCell { value: Cons(10, RefCell { value: Cons(5, RefCell { value: Cons(10, RefCell { value: Cons(5, RefCell { value: Cons(10, RefCell { value: Cons(5, RefCell { value: Cons(10, RefCell { value: Cons(5, RefCell { value: Cons(10, RefCell { value: Cons(5, RefCell { value: Cons(10, RefCell { value: Cons(5, RefCell { value: Cons(10, RefCell { value: Cons(5, RefCell { value: Cons(10, RefCell { value: Cons(5, RefCell { value: Cons(10, RefCell { value: Cons(5, RefCell { value: Cons(10, RefCell { value: Cons(5, RefCell { value: Cons(10, RefCell { 
thread 'main' has overflowed its stack
fatal runtime error: stack overflow
[1]    5255 IOT instruction  cargo run
```
_SPECTACULAR_. we got a stack overflow error. The reason is simple. We're trying to print the contents of the tail of a which means we need to show _ALL_ the links a have to the other. However, now we're in an infinite loop:
- a points to b
- the b points to a
- that a points to b
- that b points to a
- ...
This goes on forever. 
![[trpl15-04.svg|500]]
here is a depiction of the relationship between a and b. It's pretty clear why this can be troublesome.

Now that we know stuff like this is possible, how do we "cut" this loop, while still maintaining some sort of link?

## Weak links with ```Weak<T>```
Those who are keen enough might have noticed we kept counting links with ```Rc::strong_count()```, which implies the existence of ```Rc::weak_count()```. That is correct! [[Weak Count]] stems from the ```rc::Weak``` module, and this has some interesting properties:
- values can be destroyed even if there's some weak links left
- weak links does not show the actual value it points to.

If you want links but fear the cyclic/recursive nature of the link may cause memory problems, this can be a great solution.

---
Categories: [[Unsafe]], [[RefCell]], [[Smart Pointer]]
References:
Created: 2024-05-20
