---
tags:
---
# Box
Box allows you to store data on the heap. The data is stored on the heap whereas the pointer itself is stored in the stack. Boxes don't have performance overhead other than storing data in heap. Compared to other smart pointers, Boxes are relatively simple and lack any advanced capabilities.

## Usage
You may want to use Boxes in the following situations:
- type whose size can't be known in compile time but you need the exact size for
- when you have large amount of data to move ownership but you don't want to copy.
- when you want to own a value but only care for the trait it implements

## Recursive types
recursive types are types that calls itself, hence the recursion.
``` rust
enum List {
	Cons(i32, List),
	Nil,
}
```
This is a famous data structure in Lisp called ```Cons```,short for construct. 
``` rust
let it_doesnt_work: List = Cons(1, Cons(2, Cons(3, Nil)));
```
If we try to compile, the compile throws an error stating that ```the recursive l```




---
Categories: [[Smart Pointer]]
References:
Created: 2024-05-16
