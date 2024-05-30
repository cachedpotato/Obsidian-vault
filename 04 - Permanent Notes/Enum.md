---
tags: []
---
**# Enum
enum is a type that can be one of a given set of types. types within enum can be pretty much anything.
```rust
enum Message {
	Quit, //unit struct
	Write(String), //tuple struct
	ChangeColor(u8, u8, u8), //tuple struct,
	Position {x: i32, y: i32}, //struct	
}

fn main() {
	let m: Message = Message::Write(String::from("Hello"));
	//println!("{m}") <- does not work because it does not have
	//display trait
}
```

## Implementation

```rust
impl Message {
	fn call(&self) {
		match self {
			Message::Quit => println!("quitting"), //LAMBDA BOIS
			Message::Write(s) => println!("wrote {s}"),
			_ => println!("hello")
		}
	}
}

fn main() {
	let m: Message = Message::Write(String::from("hello"));
	m.call(); //will print "write hello" in stdout
}
```

## Notable Enums

There are many ways enums can be used, but here are some great enums that are included in the prelude. Option takes care of the null problem and Result is used for error handling.
### Option
```rust
enum Option<T> {
  Some(T),
  None,
}
```
Option takes care of the "billion dollar mistake", which is the null value, or lack there of. Everything will be either _something_, or _nothing_, simple as that.

#### `take` and `as_ref`
As code gets more complicated, getting and mutating values wrapped in `Option` can get confusing, take for example, a `ThreadPool` which has a vector of `Workers`, which have the actual threads:
```rust
struct ThreadPool {
	sender: Option<std::sync::mpsc::Sender<T>>,
	workers: Vec<Worker>,
}
struct Worker {
	thread: JobHandle<()>,
}
```
For graceful shutdown, we need the `ThreadPool` to join the handles and wait for all threads to finish its processes.
``` rust
impl Drop for ThreadPool {
	fn drop(&mut self) { 
		//--snip
		for worker in &mut workers {
			worker.thread.join();
		}
	}
}
```
This code will _NOT_ work, because `join` moves ownership, and we are behind a shared reference. One way of bypassing this is wrapping the worker threads with `Option`, then using the `take` method.

```rust
struct Worker {
	thread: Option<JobHandle<()>>,
}
//--snip
impl Drop for ThreadPool {
	fn drop(&mut self) {
		//--snip
		for worker in &mut workers {
			if let Some(handle) = worker.thread.take() {
				handle.join().unwrap();
			}
		}
	}
}
```
the `take()` method gets the ownership of the `thread` field, and REPLACES where it originally was with `None`. Now, the join can move ownership without any problems!

Sometimes we don't want ownership, but we do want access to the value inside.
```rust
impl ThreadPool {
	pub fn execute(&self, f: F)
	where
		F: FnOnce() + Send + 'static,
	{
		//--snip
		self.sender
			.unwrap()
			.send(job)
			.unwrap()
	}
}
```
Here we're trying to send a job to the sender which the workers will receive and execute. This will not compile, because the first `unwrap` will move the ownership of the `sender` field, which is currently behind a shared reference `&self`. What we can do, is borrow the `sender` using `as_ref`:
```rust
//--snip
self.sender
	.as_ref()
	.unwrap()
	.send(job)
	.unwrap()  
```
`as_ref` essentially converts `&Option<T>` into `Option<&T>`.

### Result
Result is an enum with 2 types:
```rust
enum Result<T, E> {
  Ok(T),
  Err(E),
}
```

If some function returns a result, it's best practice to do [[Error Handling in Rust]], which is basically taking care of error cases.

---
*Categories*: [[Rust]], [[Data Types]]
Created: 2024-05-09