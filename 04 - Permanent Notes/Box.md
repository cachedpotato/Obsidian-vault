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

To use Boxes, simply do ```Box::new()```
``` rust
let box: Box<i32> = Box::new(8);
println!("now the integer is stored in heap: {}", box);
```

## Recursive types
recursive types are types that has itself as the component.
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
If we try to compile, the compile throws an error stating that ```the recursive type List has infinite size```. In fact, the very definition of List is the root of the problem. Why does this happen?

The compiler needs to know how much memory is needed to store a variable. for enums, where only one variant is used, the compiler tries to find the maximum amount of space needed for any of the variants. in other words,
$$
memory = max_{var \in enum}\{memory_{var}\}
$$
Consider the case for the ```List``` enum above. This is what happens.
- First the compiler looks at Cons, which is a tuple of i32 and List.
- Rust then looks into List
- The compiler looks at Cons, which is a tuple of i32 and List
- Rust Looks into List
- Repeat this until the heat death of the sun.
![[trpl15-01.svg|500]]
As you can see the compiler runs infinitely, which leads into infinite memory usage error. Thankfully, besides raising error, the compiler also recommends changing the Cons structure to this:
``` rust
Cons(i32, Box<List>)
```
This is called _indirection_, which is changing the data structure to stop the value indirectly by storing a pointer to the value instead.

Now, instead of Cons being recursive, Cons is actually just a tuple with a number and a pointer that points to where to List is located in. Also, because in the stack only the pointer is stored, Rust knows exactly how much space is being used.
![[trpl15-02.svg]]

Though now actually using the List struct will look heinous:
``` rust
enum List {
	Cons(i32, Box<List>),
	Nil
}

use crate::List::{Cons, Nil}
main fn() {
	let eww: List = Cons(1, Box::new(Cons(2, Box::new(Cons(3, Box::new(Nil))))));
}
```
**CERTIFIED LISP MOMENT RIGHT HERE**. If it weren't for the ```use``` it would've been even more obnoxious. Damn.

---
Categories: [[Smart Pointer]]
References:
Created: 2024-05-16
