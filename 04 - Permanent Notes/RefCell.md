---
tags:
---
# RefCell
Whereas [[Rc]] dealt with multiple ownership and _immutable_ references, ```RefCell<T>``` deals with Interior mutability, which is a design pattern in Rust that allows you to mutate data even when there are immutable references. Typically this is not possible in Rust and is considered [[Unsafe|unsafe]]. To use unsafe code we need to tell Rust compiler that we're checking memory safety manually.

```RefCell<T>``` enforces borrowing rules at _runtime_, not compile time. This means the code will compile, but if a memory leakage happens in runtime the program will panic. Just like ```Rc```, ```RefCell<T>``` is for single-threaded scenarios only.

---
Categories: [[Smart Pointer]]
References:
Created: 2024-05-17
