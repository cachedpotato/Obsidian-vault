---
tags:
---
# Memory Allocation in C and C++
C and C++'s double edged sword is that because it's a low-level language (at least relatively speaking), we have access to memory allocation. Being able to allocate memory however we want is definitely a superpower as a coder, but it can also be one-way ticket to shooting ourselves in the foot, in the form of memory leak and memory safety issues. One simple, but VERY important rule of memory management is:

> IF YOU HAVE ALLOCATED A MEMORY, NEVER FORGET TO FREE IT AS WELL

Allocation of memory is done by `malloc` in C, and freeing is done by `free` in both C and C++

## `malloc` and `free`
`malloc` is an abbreviation for `memory allocate`, and the usage is as follows:
```C
#include <string.h>
#include <stdlib.h>

int main(void) {
	char* s = "Hello, World!";
	char* t = malloc(strlen(s) + 1);
	//--snip

	free(t);
}
```
using `malloc`, we created a memory for `t` of size the length of string `s` + 1 (+1 for the termination character `\0`). Later, with `free()`, we freed that memory space that we've allocated, so that it doesn't take up any memory and most important of all, we don't have any memory accessing issues.

One thing to note is that at the end of `main` or function calls in that matter, `free` is automatically called. However, there will be times where we want to free space before that call is given, and that's when `free` should be used. Both `malloc` and `free` are declared in the `<stdlib.h>` header file.

## `sizeof` function
while standard types such as `int` and `char` is already known, if we're trying to make arrays of custom type, we do not know exactly how much memory we need to allocate. this is where the `sizeof` function comes in. This function will automatically calculate the size of the type, and by passing this value into `malloc`, we are able to allocate the exact amount of memory we need.

```C
typedef struct {
	int x;
	char* phone_number;
	float f;
} human;

int main(void) {
	human* humans = malloc(3 * sizeof(human));
	//--snip
}
```

## Valgrind
Because memory leaks are so common when coding C/C++, there are many apps that help us find out whether there are any memory leakage, and if there are, where it's happeneing. Valgrind is one example of this, and it's relatively easy to use:
```bash
valgrind ./program
```

---
Categories: [[C++]], [[Memory Management]], [[CS50 - Introduction]]
References:
Created: 2024-06-13
