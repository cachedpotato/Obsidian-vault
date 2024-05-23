---
tags:
---
# Arc
Arc stands for "Atomic Reference Count". Because it ensures atomicity, one might wonder why they shouldn't just use ```Arc``` all the time. Unfortunately, Arc takes a hit on performance when used. We should prioritize ```Rc```, and use this only when we need atomicity.

The syntax for ```Arc``` is the same with ```Rc```.
``` rust
use std::sync::{Arc, Mutex}
use std::thread;
fn main() {
	let counter: Mutex<i32> = Arc::new(Mutex::new(0));
	let handles: Vec<thread::JoinHandle<()>> = vec![];

	for _ in 0..10 {
		let counter = Arc::clone(&counter);
		let handle = thread::spawn(move || {
			let num = counter.lock().unwrap();
			*num += 1;
		});
		handles.push(handle);
	}

	for handle in handles {
		handle.join().unwrap();
	}

	println!("Result: {}", *counter.lock().unwrap());
}
```
The key point here is that you wrap the Mutex in ```Arc``` and whenever you spawn a thread to process whatever's inside the Mutex, you use ```Arc::clone()```

## Arc and RefCell Similarities
Wait. Go back a second:
``` rust
let counter:Mutex<i32> = Arc::new(Mutex::new(0));
```
We did not set the counter variable to be mutable, but we were still able to change values within the spawned thread. This is because ```Mutex<T>``` allows internal mutability, just like. Just like how in ```RefCell<Rc<T>>``` the ```Refcell<>``` allows us to mutate values within ```Rc```, the ```Mutex<>``` in ```Arc<Mutex<T>>``` allows us to mutate values within ```Arc```.

This also means ```Mutex<T>``` allows for logic/memory errors during runtime in the form of _deadlocks_, similar to stack overflow/memory cycle issue we had with ```RefCell<Rc<T>>```.

---
Categories: [[Smart Pointer]]
References:
Created: 2024-05-23
