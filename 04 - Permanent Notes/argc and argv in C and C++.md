---
tags:
---
# Getting Arguments in C and C++
Say we have a program that runs something like this:
```bash
[...]$ ./helloword David
Hi David!
```

We passed `David` as the argument of the program, and this program simply prints it back. How do we make this work in C/C++?
Normally, we write the `main()` function like so:
```c
int main(void) {
	//--snip
}
```
however, by changing the arguments that main takes, we get access to the arguments:
``` c
int main(int argc, char* argv[]) {
	printf("hello %s !", argv[1])
}
```
`argv[]` array contains all the arguments, where `argv[0]` contains the command itself to run the program, in this case, `./helloword`. starting from `argv[1]`, we get the actual arguments put in.

Hold on. We talked about `argv`. what is `argc`? This is the value used for error handling and exit status in C/C++. the `main` function, upon successful exit, will return `0`, and if not, will return some non-zero value that is related to some error code. this value is called the _exit status_, and the `argc` is used for handling such status, to be specific, errors regarding the number of arguments.

Say a program needs ONLY 1 argument, but we provide 2. then, the `argc` value will be `3` (command + arg1 + arg2) instead of `2`. We can raise error and exit with its associated exit status accordingly.
```c
int main(int argc, char* argv[]) {
	if (argc != 2) {
		printf("ERROR: INVALID NUMBER OF ARGUMENTS");
		return 1;
		
	}
}
```



---
Categories: [[C/C++]] , [[CS50 - Introduction]]
References:
Created: 2024-06-13
