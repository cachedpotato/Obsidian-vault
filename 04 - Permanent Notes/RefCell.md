---
tags:
---
# RefCell
Whereas [[Rc]] dealt with multiple ownership and _immutable_ references, ```RefCell<T>``` deals with Interior mutability, which is a design pattern in Rust that allows you to mutate data even when there are immutable references. Typically this is not possible in Rust and is considered [[Unsafe|unsafe]]. To use unsafe code we need to tell Rust compiler that we're checking memory safety manually.

```RefCell<T>``` enforces borrowing rules at _runtime_, not compile time. This means the code will compile, but if a memory leakage happens in runtime the program will panic. Just like ```Rc```, ```RefCell<T>``` is for single-threaded scenarios only.

## ```Ref``` and ```RefMut```
```RefCell<T>``` has two different Methods that call different smart pointers:
- ```.borrow()```: Calls ```Ref<T>```, which is an immutable borrow
- ```.borrow_mut()```: Calls ```RefMut<T>```, which is a mutable borrow

Note to self: ```RefCell<T>``` in and of itself isn't really a pointer/reference, you need to borrow it first to act like a reference.

Because both types implement the ```Deref``` trait, they can be treated as regular references. In other words:
``` rust
use std::cell::{Ref, RefMut, RefCell};
let i: RefCell<i32> = 5;
let a: Ref<i32> = i.borrow();         //~ let a: &i32 = &i
let b: RefMut<i32> = i.borrow_mut();  //~ let b: &mut i32 = &mut i
```
Of course, this won't compile, because both immutable and mutable reference is valid at the same time...right? No! ```RefCell<T>``` does borrow checking at runtime!
![[스크린샷 2024-05-20 122215.png]]
```
---- tests::does_compile stdout ----
thread 'tests::does_compile' panicked at src/lib.rs:80:15:
already borrowed: BorrowMutError
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace


failures:
    tests::does_compile

test result: FAILED. 1 passed; 1 failed; 0 ignored; 0 measured; 0 filtered out; finished in 0.00s
```
As we can see, the test did run (meaning it compiled), but it panicked because of the ```BorrowMutError```. Even if we try to bypass the borrow checker in compile time, it sure as hell will come back and try to bite you during runtime.

## Interior Mutability
``` rust
let a: i32 = 5;
let r: & i32 = &a;
*r += 3; //doesnt work, obviously
assert_eq!(*r, 8);

use std::cell::RefCell;
let a: RefCell<i32> = RefCell::new(5);   //eq: let r: &a
*a.borrow_mut() += 3;                    //eq: *r += 3
assert_eq!(*a.borrow_mut(), 8);          //eq: assert_eq(*r, 8)
```
Rust's borrow checker normally denies changing a value through an immutable reference. However, with ```RefCell```, we can bypass this during compile time and let the borrow checker do its thing during runtime. If we run the bottom half of the code above, it will actually compile and run!

As explained before, this does not mean we are completely free of the wrath of the borrow checker, as it'll still enforce its rules during runtime.
``` rust
use std::cell::RefCell;
let i: i32 = 5;
let a: RefCell<i32> = RefCell::new(i);
let b: RefCell<i32> = RefCell::new(i):

a.borrow_mut();
b.borrow_mut(); //uh oh, two mutable references!
```
This will compile, but panic during runtime, because we have two mutable references at the same time. Which conveniently leads into the next session:

## Multiple mutable ownerships with ```Rc<RefCell<T>>```
Recall that ```Rc``` lets you have multiple _IMMUTABLE_ ownerships, and ```RefCell``` lets you have ONE instance of reference where interior mutability is allowed. What if we mix both? If we wrap like ```Rc<RefCell<T>>```, what would happen?

``` rust
use std::rc::Rc;
use std::cell::RefCell;

#[derive(Debug)]
enum List {
	Cons(Rc<RefCell<i32>>, Rc<List>),
	Nil,
}
use List::{Cons, Nil};

fn main() {
	let value = Rc::new(RefCell::new(5));
	let a = Rc::new(Cons(Rc::clone(&value), Rc::new(Nil)));
	let b = Cons(Rc::new(RefCell::new(3)), Rc::clone(&a));
	let c = Cons(Rc::new(RefCell::new(4)), Rc::clone(&a));

	*value.borrow_mut() += 10;
	
	println!("a after = {:?}", a);
	println!("b after = {:?}", b);
	println!("c after = {:?}", c);
}
```
Output:
```
$ cargo run
   Compiling cons-list v0.1.0 (file:///projects/cons-list)
    Finished dev [unoptimized + debuginfo] target(s) in 0.63s
     Running `target/debug/cons-list`
a after = Cons(RefCell { value: 15 }, Nil)
b after = Cons(RefCell { value: 3 }, Cons(RefCell { value: 15 }, Nil))
c after = Cons(RefCell { value: 4 }, Cons(RefCell { value: 15 }, Nil))
```

In conclusion:
- If you want to have interior mutability, wrap it with ```RefCell<T>```
- If you want to have multiple ownership, wrap that with ```Rc<T>```
- If you want multiple mutable ownership, wrap with ```Rc<RefCell<T>>```

## Differences between smart Box, Rc and RefCell

| -                     | Box | Rc  | RefCell |
| --------------------- |:---:|:---:|:-------:|
| Immutable Reference   | Yes | Yes |   Yes   |
| Mutable Reference     | Yes | No  |   Yes   |
| Multiple Ownership    | No  | Yes |   No    |
| Interior Mutability   | No  | No  |   Yes   |
| Compile Time Checking | Yes | Yes |   No    |
| Runtime Chcking       | No  | No  |   Yes   |

---
Categories: [[Smart Pointer]]
References:
Created: 2024-05-17
