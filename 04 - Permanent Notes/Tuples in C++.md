---
tags:
---
# Tuples in C++
C++ has a handy header `<tuple>` that lets us implement tuples on the fly. Declaring tuple is done by `tuple<type1, ..., typen> name` and initialization is done using the `make_tuple()` function.
```c++ 
#include <tuple>
int main() {
	tuple<int, int> a;
	auto b = make_tuple(3, 4);
}
```

## tuple operations


---
Categories: [[C++]]
References:
