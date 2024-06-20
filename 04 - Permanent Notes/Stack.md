---
tags:
---
# Stack
Stack is one of the most primitive one-dimensional data structure. Because it is 1D, it shares, or rather contains, features that can be found in normal arrays, but stacks have its own spin on thigs: Last In, First Out (LIFO). As the name suggests, whatever's been added to the stack at the end, will be "popped" out first.
![[stack.webp|500]]
FILO data structures might seem inconvenient at best at first glance, but this very structure is how computer handles its processes and why they are so fast!

## Memory Stack
Let's take a very simple code that stores data and calls a function:
``` rust
fn called(x: i32) -> i32 {
	let n: i32 = x + 1
	called_within_call(n)
}

fn call_within_call(n: i32) -> i32 {
	n * 2
}

fn main() {
	let x: i32 = 4;
	let y: i32 = called(x);
	println!(y);
}
```

As we've said before, computer stores data/functions in the form of stacks. to be more precise, the stack looks something like this:
![[th-2874616218.jpg | 350]]
For now we'll only be looking at the stack portion. The stack will first store the _Return address_ of each function. next, it will store the local variables. Note that the `main()` function will be the first to be called, so in this case x will be pushed, then y. but now, y calls the function `call1`. The stack will push the `call1()` function's parameters `x`, and its return address. This calls another function `call2`, where similar things happen. after `call2()` _RETURNS_ a value, the block containing the `call2()` function instructions will be popped, then using stack pointer, will return to `call1()`. after this returns a value, the stack will be popped and moved to `main()` once more. This process is done until the program is complete.

This is a mouthful, but let's simplify this into how the "function call stack" looks like:
              `call2`
       `call1`  `call1`  `call1`          `println!` 
`main`   `main`   `main`   `main`   `main`   `main`   `main`

we can see that _THE LAST FUNCTION TO BE PUSHED INTO THE STACK IS POPPED FIRST_, hence the name "memory _stack_".

## When to use stack?
Stacks are very versatile and can be used in a lot of situations. Whenever some sort of FILO mechanism needs to be used, stacks should be one of the very first data structure to consider.

However, this is easier said than done - exactly WHEN do we need FILO?
We can interpret FILO in this way: whatever comes last, will affect the one before. So, to get the final value, we need to do some computation on a "higher level" first, then move "downwards". In other words, stacks can be used to obtain a "low level" result with "higher level" dependencies.

Examples include:
1) [[Depth First Search Algorithm]] algorithm, where we find a certain path to the answer using "trees"
2) Pathfinding/simulating with tree structure
3) Cases where backtracking in arrays are involved
4) Cases where "innermost" thing needs to be computed first
	1) Parentheses
	2) Calculation

## Key stack methods
for stacks to be well, stacks, two key methods must be incorporated:
- `push()`: for pushing a value on the _top_ of the stack
- `pop()`: for removing the _top_ value of stack
``` rust
trait Stack<T> {
	type Error;
	fn push(&mut self, val: T);
	fn pop(&mut self) -> Result<T, Self::Error>;
}

struct MyStack {
	stack: Vec<i32>,
}

impl Stack<i32> for MyStack {
	type Error = String;
	fn push(&mut self, val: T) {
		self.push(val); //redundant I know
	} 
	fn pop(&mut self) -> Result<T, Self::Error> {
		if self.stack.len() == 0:
			return Err("stack already empty".into())
		else:
			n: i32 = self.stack[-1]
			self.stack = self.stack[:self.stack.len() - 1]
			return Ok(n)
}
```




---
Categories: [[Data Structure]]
References: https://www.programiz.com/dsa/stack
Created: 2024-06-10
