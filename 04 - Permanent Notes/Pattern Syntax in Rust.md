---
tags:
---
# Pattern Syntax in Rust
Here are a collection of syntax valid in patterns.

## Matching literals
``` rust
let x = 5;
match x {
	1 => println!("one"),
	_ => println!("not one"),
}
```
Pretty standard case of matching against literals.

## Matching named variables
``` rust
let x = Some(10),
let y = 5;

match x {
	Some(50) => println!("fifty"),
	Some(y) => println!("some other value {}", y),
	_ => println!("default case, {:?}", x),
}
```
Let's focus on the second arm. What do you think will happen? It actually does _NOT_ try to match the value 5 declared above, this is a new variable within the ```match``` scope that will bind to any value that is not 50 if x is ```Some(n: i32)```. That means, the following code will result in:
```
some other value 10
```
, and not 
```
default case: Some(10)
```

## Multiple Patterns
we can use the OR operator `|` to match multiple patterns
``` rust
let x = 10;
match x {
	3 | 10 => println!("three or ten"),
	5 => println!("five"),
	_ => println!("default case"),
}
```

## Range of values
we can use `..` or `..=` to match range of values. The = sign is for matching the end case. Remember, `a..b` does not include b, but `a..=b` does.
``` rust
let x = 10
match x {
	1..3 => println!("one to two"),
	3..7 => println!("three to six"),
	8..=10 => println!("eight to ten"),
	_ => println!("default")
}
```


## Advanced Pattern Syntax
So far we've covered basic syntax for pattern matching. Here are some of the more "advanced" syntaxes worth their own notes.
- [[Destructuring in Rust]]
- [[Match Guard]]
- [[Ignoring Values in Pattern Matching]]
- [[@ Bindings]]

---
Categories: [[Pattern Matching in Rust]]
References:
Created: 2024-05-24
