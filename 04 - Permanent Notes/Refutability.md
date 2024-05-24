---
tags:
---
# Refutability
An irrefutable pattern is a pattern that _CANNOT FAIL_. for example,
``` rust
let x = 5;
```
this cannot fail because x is the whole pattern. whatever's on the right hand side, WILL bind to x.

On the other hand, a refutable pattern is a pattern that _MIGHT FAIL_, such as the ```if let``` statements:
``` rust
let a: Result<_, _> = result_maker(3);
if let Ok(_) = a {println!("Success")};
```
a might be an ```Ok()``` or an ```Err()```, so the pattern matching can fail.

Most of the time we don't need to think about refutability as it's quite obvious. However, problems may arise when you use refutable pattern in places where you need irrefutable pattern, and vice versa. Below is a simple table of when you should use what refutability:

| Refutable | Irrefutable |
| --------- | ----------- |
| if let    | let         |
| while let | for         |


---
Categories: [[Pattern Matching in Rust]]
References:
Created: 2024-05-24
