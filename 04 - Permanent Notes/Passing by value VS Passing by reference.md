---
tags:
---
# Passing by value VS Passing by reference
Consider this simple swapping function:
```C
void swap(int x, int y);

int main(void) {
	int x = 10;
	int y = 15;
	swap(x, y);
	printf("x: %i, y: %i\n", x, y);
}

void swap(int x, int y) {
	int temp = x;
	x = y;
	y = temp;
}
```
we swapped the two values `x` and `y`, but running this results in:
```
$ ./swap
x: 10 y:15
```
why? we did swap the values in the function, but the values remain the same. This is because we swapped at the wrong scope.

This current function passes the x and y by _VALUE_, meaning it essentially creates a new variable with the same value passed through the function. because we are essentially swapping values only in the scope of this function, the actual values of `x` and `y` is not swapped. If only there is a way to access the exact address of these integers and swap them there...

Oh right.

REFERENCES!

```C
//--snip
int main() { 
	int x = 10;
	int y = 15;
	swap(&x, &y);
	printf("x: %i, y: %i\n", x, y);
}

void swap(int* x, int* y) {
	int temp = *x;
	*x = *y;
	*y = temp;
}
```
See how the function takes a _REFERENCE_ to the values? this is called _passing by reference_. If we want to change the values stored in that memory, we need to pass them by reference, and mutate the value within the function via dereferencing.

---
Categories: [[C/C++]], [[CS50 - Introduction]]
References:
Created: 2024-06-13
