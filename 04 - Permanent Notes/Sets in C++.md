---
tags:
---
# Sets in C++
C++ provides `unordered_set` and `set` to for implementing sets. Note that the types set can hold are limited - it must be _hashable_. This means [[Arrays in C and C++|arrays and vectors]] cannot be stored inside a set as they can change values and order. We can use [[Tuples in C++|tuples]] instead.

```c++
#include <set>
using namespace std;
int main() {
	set<int> mySet;
	mySet.insert(1);
	mySet.insert_range({1, 2, 3, 4}); //insert multiple values
	mySet.remove(1);
	mySet.find(1);
	mySet.clear(); //remove all elements
}
```


---
Categories: [[C++]]
References:
