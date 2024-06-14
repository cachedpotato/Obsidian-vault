---
tags:
---
# Pointers in C and C++
_HOO BOY_. Here we go again.
Pointers, in essence is just an integer that holds the address of some value. that value can be of any type, be it `char`, `int`, or even custom type with `struct`, pointer points to the address of that value, or the first element of the sequence of values.

One example of this is strings. Strings are just a sequence of characters that reside in the heap. Therefore, we can have a `char` pointer that points to the first character of the string, like so:
```C++
int main(void) {
	char* string = "Hello, World!";
	int n = 10;
	int* p = &n;
	printf("The address at %p has the value %d", p, *p);
}
```
The code snippet above also shows how to print the address of the value, the type syntax and how to dereference the pointer. when we declare a pointer, we do it like so: `(type)* ptr_name;`. To reference a value, we add the ampersand `&`, and to dereference the value, we add the asterisk.

- when `*` is at the left hand side: It's used to declare a pointer
- when `*` is at the right hand side: It's used to dereference.

Of course, we can create pointer that points to a pointer:
```C++
int main(void) {
	int n = 10;
	int *p = &n;
	int** pp = &p;

	printf("%p %d", *pp, **pp);
}

```

## The `->` operator


---
Categories: [[C/C++]], [[CS50 - Introduction]]
References:
Created: 2024-06-13
