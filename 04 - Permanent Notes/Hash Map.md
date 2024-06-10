---
tags:
---
# Hash Map
Hash map can be thought of as a collection of (key, value) pairs. key can be anything that can be indexed (which varies from language to language) and values are the data we want to actually store. The "key" of hash maps (pun 100% intended) is that we can search the value we desire with the key portion of the pair, and this can be done in **O(1) TIME**. When it comes to search time complexity, there's little to none that is as efficient as hash maps.

## Structure and Hash Function
Hash functions are what makes this all possible. We enter a key, the key undergoes some changes with the hash function, and we point to whatever that function returns, which contains the address of the stored data. Therefore, Hash Map can be summarized into this one picture:
![[Pasted image 20240610104220.png]]
Depending on the use case, having multiple values in the same index can be desired or can be an artefact of something known as cramming, where the hash function erroneously maps different keys to the same value.

## When to use Hash Maps?
Umm... **Anywhere?**. Hash map's O(1) search time is EXTREMELY powerful, and is used in a very wide variety of situations. Hash Maps can be extra helpful for things such as:
1) Storing count data: track how many times the key appears in a list
2) Data where searching is the primary focus (fast lookup time required)

Of course, hash maps are not without its drawbacks - it's relatively big in size, and most of all, hash maps must be stored in the heap, which means while yes the searching is O(1), it is still slower than searching inside the memory stack. If your data will keep changing size and/or is big, consider using hash maps. If not, then fixed-size arrays can be sufficient.

---
Categories: [[Data Structure]]
References:
Created: 2024-06-10
