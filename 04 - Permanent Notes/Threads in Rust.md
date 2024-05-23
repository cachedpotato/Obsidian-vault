---
tags:
---
# Threads in Rust
OS separates a given process into multiple parts, and if possible will run them simultaneously. This is done by using threads. The same thing can apply to code. Rust has various methods/features for concurrency and parallelism. Let's start with the basics of threads.

## Creating a new thread
You can create thread with the ```thread::spawn``` method
``` rust
use std::thread;
use std::time::Duration;

fn main() {
	thread::spawn(||{
		for i in 1..10 {
			println!("hi number {} from the spawned thread", i);
			thread::sleep(Duration::from_millis(1));
		}
	});

	for i in 1..5 {
		println!("hi number {} from the main thread", i);
		thread::sleep(Duration::from_millis(1));
	}
}
```
We can see the ```spawn()``` method takes a [[Closure|closure]] as input. Now let's look at the output.
```
hi number 1 from the main thread
hi number 1 from the spawned thread
hi number 2 from the main thread
hi number 2 from the spawned thread
hi number 3 from the main thread
hi number 3 from the spawned thread
hi number 4 from the main thread
hi number 4 from the spawned thread
```
We can see the program prematurely ended without waiting for the thread to be fully executed, nor is it in any coherent order. the order in which process is executed differs by kernel, CPU, situation, sleep time, etc. 

To make the program wait till the thread fully finishes its process, we need to give the thread a let binding. the ```spawn``` method actually returns a ```JoinHandle``` instance, and we can use the ```join()``` method to make the program process all thread operations:
``` rust

use std::thread;
use std::time::Duration;

fn main() {
	let handle: JoinHandle = thread::spawn(||{
		for i in 1..10 {
			println!("hi number {} from the spawned thread!", i);
			thread::sleep(Duration::from_millis(1));
		}
	});

	for i in 1..5 {
		println!("hi number {} from the main thread!", i);
		thread::sleep(Duration::from_millis(1));
	}

	handle.join().unwrap();
}
```
Result
```
hi number 1 from the main thread!
hi number 2 from the main thread!
hi number 1 from the spawned thread!
hi number 3 from the main thread!
hi number 2 from the spawned thread!
hi number 4 from the main thread!
hi number 3 from the spawned thread!
hi number 4 from the spawned thread!
hi number 5 from the spawned thread!
hi number 6 from the spawned thread!
hi number 7 from the spawned thread!
hi number 8 from the spawned thread!
hi number 9 from the spawned thread!
```

## Using ```move``` closure
As we've seen before, we do not know when and how thread processes will be executed. Meaning, if we try to capture an environmental variable within the closure, because closures try to take reference rather than take full ownership, this will cause an error because the compiler does not know how long the thread will last.

This is why we need to force the closure to take ownership of the captured variable with ```move```.
``` rust
fn main() {
	let v: Vec<i32> = vec![1, 2, 3];
	let handle = thread::spawn(move || {
		println!("captured the vector: {:?}", v);
	});

	//drop(v); //this will cause compiler error
	           //because ownership has been moved to the closure

	handle.join().unwrap();
}
```


---
Categories: [[Rust]], [[Concurrency]], [[Parallelism]]
References:
Created: 2024-05-22
