---
tags:
---
# Message Passing in Rust
One increasingly popular approach to ensuring safe concurrency is message passing. Ergo, "Do not communicate by sharing memory; share memory by communicating".

Rust provides ```mpsc```, short for "multiple producer, single consumer", for message passing. As the name suggests, there can be multiple transmitters in the channel, but only one receiver.

## The ```mpsc```
Below is a simple use case of ```mpsc```:
``` rust
use std::sync::mpsc;
use std::threads;

fn main() {
	let (tx, rx): (Sender<String>, Receiver<String>) = mpsc::channel();

	thread::spawn(move || {
		let val = String::from("hi");
		println!("from transmitter: {}", val);
		tx.send(val).unwrap();
		//println!("from transmitter: {}", val); <- borrow error
	});

	let received: String = rx.recv().unwrap();
	println!("received from transmitter: {}", received);
	
}
```
We first get the transmitter (```tx```) and receiver (```rx```) via de-structuring the ```mpsc::channel()``` function. Then we can transmit and receive data by ```send()``` and ```recv()``` respectively. Note that both functions return Result, so you need to unwrap it first.

## Multiple Producer, Single Receiver
We can set multiple producer for a given channel using the ```clone``` method.

``` rust
use std::threads;
use std::sync::mpsc;
use std::time::Duration;

fn main() {
	let (tx: Sender<String>, rx: Sender<String>) = mpsc::channel();
	let tx1 = tx.clone();
	
	threads::spawn(move || {
		let vals: Vec<String> = vec![
			String::from("hi"),
			String::from("from"),
			String::from("transmitter"),
			String::from("one"),
		];
	
		for val in vals {
			tx1.send(val).unwrap();
			thread::sleep(Duration::from_milli(1));
		}
	});
	
	threads::spawn(move || {
		let vals: Vec<String> = vec![
			String::from("from"),
			String::from("yet"),
			String::from("another"),
			String::from("transmitter"),
		];
	
		for val in vals {
			tx.send(val).unwrap();
			thread::sleep(Duration::from_milli(1));
		}
	});

	for received in rx {
		println!("received: {}", received);
	}
}
```
Unlike the previous example where we called the ```recv()``` function, we are using ```rx``` as the iterator. Also note that while there may be multiple transmitter, there can be only one receiver. Anyways, here's the result:
```
received: hi
received: from
received: from
received: transmitter
received: one
received: yet
received: another
received: transmitter
```
As with normal thread processing, the order is highly variable.

---
Categories: [[Threads in Rust]], [[Concurrency]]
References:
Created: 2024-05-22
