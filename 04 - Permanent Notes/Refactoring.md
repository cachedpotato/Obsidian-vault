---
tags:
---
# Refactoring
as projects get bigger, the main binary file gets bigger as well. at some point, it will become hard to read. in this situation, it's better to split it up into little pieces to make things modular, and move it to somewhere else in the library. this organization process is called refactoring.

some general rules for refactoring 
- split your main program into main.rs and lib.rs, moving your program's logic to lib.rs
- the command line parsing logic stays in main.rs unless that too gets too complicated.

the main.rs file has the following responsibilities
- calling command line parsing logic
- setting up extra configs
- calling a run function in lib.rs (the main logic behind the program)
- error handling if ```run``` returns an error

Refactoring goes in tandem with [[Paths|modules file management]].


---
Categories: [[Programming]] 
References:
Created: 2024-05-15
