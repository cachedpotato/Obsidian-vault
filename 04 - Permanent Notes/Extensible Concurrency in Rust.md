---
tags:
---
# Extensible Concurrency in Rust
Rust has very few concurrency features. However there are some [[Traits in Rust|traits]], namely ```std::marker::Sync``` and ```std::marker::Send``` for us to customize our own concurrency. It is worth noting that both using these traits manually is considered [[Unsafe]].

## ```Send``` trait
the ```Send``` trait indicates that ownership of values of the type with this trait can be transferred between threads. Almost all Rust type has this trait, except for some exceptions.
```Rc<T>``` does _NOT_ have this trait, because there is a chance multiple threads can update the reference count at the same time.
Raw pointers also do not have this trait.

## ```Sync``` trait
The ```Sync``` trait indicates that it is safe for the type with this trait to be _referenced_ from multiple threads. Recall the ```Send``` trait deals with transferal of _ownership_ between threads. The connections are clear:
-  Any type T is ```Sync``` if &T is ```Send```
[[Shared State Concurrency|As we've seen before]], ```Mutex<T>``` can be shared between threads, so it has this trait. However, ```RefCell<T>```'s runtime borrow-checking is not safe, therefore it does not have this trait.





---
Categories: [[Concurrency]], [[Traits in Rust]]
References:
Created: 2024-05-23
