---
tags:
---
# Closure
A closure is an _anonymous function_ you can save in a variable or pass as arguments to other functions. Closures have the unique ability to capture values from the scope they're defined in, which functions can't do. Closures are meant to be byte-sized, so don't overcomplicate things!

## Key differences between function and closure
- Closures can capture and pass values within its own scope
- Closures normally does not require type annotations

## Inference of Types in closures
closures don't need type annotations. The compiler will infer one concrete  type for each of their parameters and for their return value the first time it is used. _THIS CANNOT BE CHANGED_.

``` rust
let exapmple_closure = |x| x;
let s = example_closure(String::from("hello"));
let n = example_closure(10);  //this will raise error
```
during the creation of ```s```, the closure's input (and also output in this case) will be hard set to String. Because this is not changeable, when we try to pass an integer to the same closure after this, it will raise error.

## Capturing Values in closures
Closures can capture values from their environment three ways: 
- Borrowing immutably
- Borrowing mutably
- Taking Ownership
...Wow. Shockers. The closure decides which of these should be used based on what the body of the function does. Closures will try to pick the _least invasive_ option if given multiple choices. Invasiveness order is as follows:
- immutable borrow < _mutable borrow_ < **Taking Ownership**

``` rust
let list = vec![1, 2, 3];
println!("before defining closure: {:?}", list);
let closure = || println!("we're in closure {:?}", list);

println!("before closure: {:?}", list);
closure();
println!("after closure: {:?}", list);
```
The output will be:
```
before defining closure: [1, 2, 3]
before closure: [1, 2, 3]
we're in closure [1, 2, 3]
after closure: [1, 2, 3]
```
As we can see, the closure did not take ownership of the list, as the closure opted to select the least invasive option, which is immutable borrow in this case.

Also note that the ```list``` here was captured in the _BODY_ of the closure, not the input argument. The concept of capturing is not limited to inputs, but also the main body as well.

```rust
let list = vec![1, 2, 3];
println!("before defining closure: {:?}", list);
let closure_2 = || list.push(4);
closure();
println!("after closure: {:?}", list);
```
Output:
```
before defining closure: [1, 2, 3]
after closure: [1, 2, 3, 7]
```
The closure mutably borrowed the list in this case, but still did not take ownership.
because a mutable reference to list is made _when the closure is defined_, we can't print the list by passing another mutable reference.

To force a closure to take ownership, use the ```move``` keyword
``` rust
use std::thread;
fn main() {
	let list = vec![1, 2, 3];
	println!("before defining closure: {:?}", list);
	thread::spawn(move || println!("from thread: {:?}", list))
		.join()
		.unwrap()
}
```

## Moving captured values out of the closure
Once a closure has captured a value from the environment where the closure is defined, the code in the body of the closure defines what happens to the captured values when the closure is evaluated after. A closure can do any of the following:

- move a captured value out of closure
- mutate captured value
- neither move nor mutate captured value
- capture nothing from the environment

closures implement different traits depending on how it captures/handles environment values. Closures can capture any of the three [[Fn Traits]].



---
Categories: [[Rust]], [[Functional Programming]]
References:
Created: 2024-05-15
