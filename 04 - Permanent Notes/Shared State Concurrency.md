---
tags:
---
# Shared State Concurrency
While message passing is a safe and effective way to share memory, there are times we might want to have multiple ownership for a given memory. Message passing does not allow that in a fundamental level, because there can only be one receiver.

We've seen before that [[Rc]] can make multiple ownership possible for _single-threaded_ operations, which means its incompatible with concurrency. Instead, we will use what's called Mutex and yet another smart pointer called ```Arc```.

## Mutex
[[Mutex]] is an abbreviation for "mutual exclusion". If one is using data, no other processes can touch it, hence the mutual exclusion. This is implemented by using what's referred to as locks. The rules are simple:
- When a process is accessing a Mutex data, first they need to aquire the lock.
- No other processes can manipulate the data when the Mutex is in locked state.
- Once the process is done, it must unlock the Mutex.

Let's see how Rust handles Mutex.
``` rust
use std::sync::Mutex; //mpsc is also in sync module!

fn main() {
	let m: Mutex<i32> = Mutex::new(5);
	println!("m before: {:?}", m);

	{
		//aquire lock
		let mut num: MutexGuard<i32> = m.lock() //Result<MutexGuard<i32>, PoisonError<i32>>
			.unwrap() //MutexGuard<i32>
		*num = 6;
	} //Mutex<T>::drop() called here

	println!("m after: {:?}", m);
}
```
Result:
```
m before: Mutex { data: 5, poisoned: false, .. }
m after: Mutex { data: 6, poisoned: false, .. }
```

Mutex is a generic type that, when ```lock()``` is called upon, returns a smart pointer ```MutexGuard<T>``` wrapped in Result. To access the value, we can dereference the pointer as with any other pointers.

from the standard out we can see the ```Mutex<T>``` does not simply have the value, but also have other fields, such as ```poisoned```. The "Poison" here means that the lock has already been acquired somewhere else.

To print the value (data) only, we need to dereference the Mutex just like we did to manipulate data
``` rust
//-snip
println!("Just the value: {}", *m.lock().unwrap());
```
Note that we still need to acquire the lock to print out its value.
Let's move on to some multi-threaded usage of Mutex.

## Multithreaded use case
``` rust
fn main() {
	let counter = Mutex::new(0);
	let mut handles = vec![];
	
	for _ in 0..10 {
		let handle = thread::spawn(move || {
			let mut num = counter.lock().unwrap();
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
This will not compile, and give the following error:
```
$ cargo run
   Compiling shared-state v0.1.0 (file:///projects/shared-state)
error[E0382]: borrow of moved value: `counter`
  --> src/main.rs:21:29
   |
5  |     let counter = Mutex::new(0);
   |         ------- move occurs because `counter` has type `Mutex<i32>`, which does not implement the `Copy` trait
...
9  |         let handle = thread::spawn(move || {
   |                                    ------- value moved into closure here, in previous iteration of loop
...
21 |     println!("Result: {}", *counter.lock().unwrap());
   |                             ^^^^^^^ value borrowed here after move

For more information about this error, try `rustc --explain E0382`.
error: could not compile `shared-state` (bin "shared-state") due to 1 previous error

```
The counter variable was moved into the thread closure. This is why when we try to re-borrow it to print out the result, the compile will give the "borrow of moved value" error. Essentially, we can't just give multiple ownership to Mutex locks.

One can think of Using ```Rc``` as a workaround for this issue, but the compiler will give another lengthy error saying:
```
cargo run
   Compiling shared-state v0.1.0 (file:///projects/shared-state)
error[E0277]: `Rc<Mutex<i32>>` cannot be sent between threads safely
```

```Rc``` does not use any concurrency primitives to make sure that changes to reference count can't be interrupted by another thread. This may lead to wrong borrow counts, and ultimately memory leaks.

What we need to use instead, is an Reference Counter with atomicity. Thankfully, Rust has just that - yet another smart pointer called [[Arc]].

---
Categories: [[Concurrency]], [[Rust]], [[Mutex]]
References:
Created: 2024-05-23
