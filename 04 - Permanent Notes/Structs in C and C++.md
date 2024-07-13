---
tags:
---
# Structs in C and C++
While C++ is the "Objected Oriented Approach" applied to C, that does not mean C does not even have structs. It does, but with limitations. The syntax is also different as well.

1) C
``` c
typedef struct {
	int age;
	char name[];
}person;
```

2) C++
```C++
struct person{
	int age;
	string name;
};
```

## constructor overloading
like [[Classes in C++|classes,]] we can create custom constructors for structs, and even overload them. Here's an example:
```c++
struct TreeNode {
	int val;
	TreeNode* left;
	TreeNode* right;

	//constructor overloading
	TreeNode(): val(0), left(nullptr), right(nullptr) {}
	TreeNode(int x): val(x), left(nullptr), right(nullptr) {}
	TreeNode(int x, TreeNode* left, TreeNode* right) {
		val = x;
		left = left;
		right = right;
	}

	int main() {
		TreeNode a();
		TreeNode b(1);
		TreeNode c(2, &a, &b);
	}
}
```

---
Categories: [[C++]], [[CS50 - Introduction]]
References:
Created: 2024-06-13
