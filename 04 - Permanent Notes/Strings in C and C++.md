---
tags:
---
# Strings in C and C++
strings in C, like in all other languages (except for I guess Rust which handles strings a lot differently), are essentially an array of `char`s . 
```c
char hi[5] = "hello";
printf("%c", hi[0]) //prints 'h'
```

Like in any other arrays, the very first character is stored at index 0, and the very last character "that we care about" is stored at index `len(s) - 1`. However, this is actually _NOT_ the actual character in this array!
```c
char hi[5] = "hello";
printf("%i", hi[5]) //prints 0
```
the length of the string we provided is 5, so accessing `hi[5]` should in theory return `segmentation fault` error, but instead it returns 0. To be exact, this is not actually 0, but it can be thought of as a "terminator" to indicate that the string ends here.

To summarize, given a string of length n:
- index 0 ~ `len(string) - 1 `: characters of string
- index n: terminator, or `\0`.

While yes you CAN access this, it's best to always access only the characters we care about, as pointers pointing to places it really shouldn't be will result in nasty memory errors and at worst puts your computer at risk.


---
Categories: [[C++]], [[Data Types]], [[CS50 - Introduction]]
References:
Created: 2024-06-13
