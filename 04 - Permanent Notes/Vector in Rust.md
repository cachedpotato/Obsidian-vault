---
tags:
  - Rust
---
# Vector in Rust
vectors can only hold values of the same type.
```rust
let v1: Vector<u8> = Vector::new();
let mut v2 = vec![1, 2, 3]; //ints will default to i32 I believe?

//add elements
v2.push(4);
v2.push(5);
v2.push(6);
```
Note how we don't mention size when we create a vector. This is because unlike arrays or tuples, we can change its size (insert or delete elements). This is why vectors are stored in heap.

## reading elements
there are two ways of referencing a value stored in vector:
- indexing
- ```get``` method
```rust
let v: Vector<usize> = vec![1, 2, 3, 4, 5];
let ref1: &usize = &v[0];
let ref2: Option<&usize> = v.get(0);
```
As the elements of this vector are of the type ```usize```, the reference type will be ```&usize```, not ```&Vector```. the get method will return an Option type, so to use the value inside you must unwrap it first or use pattern matching. the advantage of using ```get``` is that in case of an index OOS error, it will just give None as the output instead of the whole program panicking:
```rust
let none = v.get(100);
match none {
	Some(_n) => println!("wait what"),
	None => println!("index out of bounds")
}
//v[100]; <- this will panic
```

## The ```push``` method
one thing to be cautious about is that push will output a _MUTABLE REFERENCE_. regular reference/borrowing rules apply here.
```rust
let mut v = vec![1, 2, 3];
let r: &i32 = &v[0]; //immutable reference
v.push(4); //mutable reference
println!("uh oh, {r}"); //<- immutable reference called again, compile error
```

## Iterating over values
```rust
let mut v = vec![10, 20, 30];
for i in &v { //i is of the type &i32
	println!("{i}");
}
for i in &mut v {
	*i *= 2; //we must dereference it first
	println!("element changed to {i}");
}
```
as mentioned above, the ```i``` iterator in the for loop is of type &vector_element_type. when mutating vector element values, we must dereference the iterator first.

## A workaround for the one-type limit
Each variants (elements? values?) in an enum is still considered the same type. We can use this to our advantage, especially with vectors. What if we want a vector with strings, integers and floats? Well, just make an Enum with exactly those.
```rust
enum VectorWorkaround {
	Int(i32),
	Float(f64),
	Text(String),
}

let snarky_vector: Vec<VectorWorkaround> = vec![
	VectorWorkaround::Int(3),
	VectorWorkaround::Text(String::from("We chillin")),
	VectorWorkaround::Float(0.669),
];

for i in &snarky_vector {
	match i { //no need to dereference I guess? idk coding is hard
		VectorWorkaround::Float(n) => println!("floaty boi: {n}"),
		VectorWorkaround::Int(n) => println!("integer too: {n}"),
		VectorWorkaround::Text(s) => println!("wait text also? {s}")
	}
}
```



---
Categories: [[011-Rust]], [[Data Types]]
References:
Created: 2024-05-12