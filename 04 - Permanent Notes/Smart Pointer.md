---
tags:
---
# Smart Pointer
_WE ARE NOW REACHING LEVELS OF STINKY WE NEVER THOUGHT POSSIBLE_
Pointers is a concept for a variable that contains an **address** in memory that _points_ to some other data. a [[Reference]] is a type of pointer, a very common one at that, in Rust. A _smart pointer_ is a pointer with extra metadata and capabilities. Think of function pointers in C/C++. 

Because of Rust's unique concept of ownership and borrowing, Rust's smart pointers have additional differences between references, such as having ownership of the data they point to. Examples of such smart pointers that we have already covered are ```String``` and ```Vec<T>```. These are pointers that point to a data in heap, but they also _OWN_ the data. ```String``` also has additional metadata, such as encoding (UTF-8). 

Smart pointers are usually implemented using structs, and also implement [[The Drop Trait]] and [[The Deref Trait]]. 
- ```Deref``` lets the smart pointer to act like a reference to help your code work with references
- ```Drop``` trait allows you to customize the code that's run when an instance of the smart pointer goes out of scope.

As powerful as they are, because they toy around with ownerships, abusing these will lead to **UNSAFE CODE**. Be careful when you use these!
## Examples
Examples of Smart pointers include: 
- [[Box|Box<T>]], for allocating values on the heap

- [[Rc|Rc<T>]], a reference counting type that enables _MULTIPLE OWNERSHIP_

- [[Arc|Arc<T>]], the reference counting smart pointer with atomicity.
- ```Ref<T>``` and ```RefMut<T>```, accessed through [[RefCell|RefCell<T>]], a type that enforces the borrowing rules at _RUNTIME_
- ```MutexGuard<T>```, accessed through [[Shared State Concurrency|Mutex<T>]], used for concurrent processing


---
Categories: [[Rust]], [[Pointer]] 
References:
Created: 2024-05-16
