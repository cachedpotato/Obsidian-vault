---
tags:
---
# Tries
We have briefly mentioned in [[Hash Map|hash maps]], but searching in hash map isn't _TECHNICALLY_ `O(1)` time because of collisions, where hash functions return the same value for different keys. A trie, aims to solve this problem, by pretty much adding an IMMENSE amount of space.

A trie (funny name I know) is pretty much a map of arrays or nodes. The way how tries solve the collision problem in hash map is that given a key, we split that key into the most basic element (example: character given a string), and then using these components, we go down this map of arrays until we reach the end (end is indicated by an internal value), where the actual value is stored. It's quite a mouthful to say, but to visualize, a trie would look something like this:
![[trie-data-structure-1963877449.png | 500]]
While yes this will ensure our searching is done in O(1) time, where the maximum time required would be the length of the longest key, as we can see here it takes up an IMMENSE amount of space.


---
Categories: [[Data Structure]], [[CS50 - Introduction]]
References:
Created: 2024-06-13
