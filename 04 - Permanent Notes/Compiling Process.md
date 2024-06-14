---
tags:
---
# Compiling Process
Compiler Language goes through 4 big steps to create the final (often times) executable files
1) preprocessing: in C/C++, preprocessing commands are annotated with  `#`, such as `#include` or `#pragma once`.
2) compiling: compiling turns this into translatable machine code, also known as assembly. Optimization is done during this process.
3) assembling: takes assembly code into 0s and 1s that computer understands
4) linking: combines the created 0s and 1s that the computer understands together into a one big executable file

reverse engineering machine code back into the original source code is a lot easier said than done, but you can still get a general glimpse of how things work, how memories are stored, etc.

---
Categories: [[Compiler]], [[CS50 - Introduction]]
References:
Created: 2024-06-13
