---
tags:
---
# Arrays in C and C++
There are multiple ways of implementing arrays in C/C++. C++ introduced the `<vector>` and `<stack>` header making things a lot easier than trying to wrap our head around with `malloc`, but it's good to start with the basics first.
## Default Array
To initialize an array in C/C++, the syntax is `type name[size]`.
```C
char myString[10];
int myIntArray[5];
```
To initialize, we use curly braces, NOT `[]`.

```c++
int myIntArray[5] = {1, 2, 3, 4, 5};
//partial initialization
int anotherArray[5] = {1, 2};
//No need to specify size as well!
//the size will be decided based on the initialization
int yetAnotherArray[] = {1, 2, 3, 4, 5};
```
## Vector
the `Vector` type in C++ comes with nice methods like `push_back` and is also dynamically sized.
``` C++
#include <vector>
with namespace std;
int main() {
	vector<int> myVector;
	//dynamically sized!
	myVector.push_back(1);
	myVector.push_back(2);
	myVector.push_back(3);
	myVector.push_back(4);

	myVector.pop_back();
	myVector.erase(myVector.begin() + 2) //remove third element (a[3])

	for (auto &r: myVector) {
		cout << r << endl;
	}
}
```

## Subarrays
There are multiple ways to splice arrays/vectors into subarrays, but the easiest way is to use the splice constructor with `begin()` and `end()` methods.
```c++
int main() {
	vector<int> v;
	v.push_back(1);
	v.push_back(2);
	v.push_back(3);
	v.push_back(4);
	v.push_back(5);

	vector<int> first_two = v(v.first(), v.first() + 2);
	vector<int> latter_half = v(v.first() + 2, v.end());
}
```
This is the same as
```python
v = [1, 2, 3, 4, 5]
first_two = v[0:2];
latter_half = v[2:];
```
This also works well with `find` function:
```c++
int main() {
	auto m = find(v.begin(), v.end(), 3);
	vector<int> till_three = v(v.begin(), v.begin() + m + 1);
}
```



---
Categories: [[C++]] 
References:
