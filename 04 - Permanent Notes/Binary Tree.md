---
tags:
  - NeedWork
---
# Binary Tree


## Implementation
```C
typedef struct Node {
	int val;
	struct Node* left; //smaller
	struct Node* right; //bigger
} Node;

void add_to_tree(Node* tree);

int main(void) {
	Node* tree = malloc(5 * sizeof(Node));
	//--snip
}
```

## Searching in Binary Tree
Binary trees have a unique property of the left daughter node being smaller than the parent node, and the right daughter node being bigger than the parent node. Using this, we can create a recursion algorithm for searching in `O(logn)` time.
```C
bool search(Node* tree, int target) {
	//base case
	if (tree == NULL) {
		return False;
	} else if (target < tree.val) {
		return search(tree -> left, target);
	} else if (target > tree.val) {
		return search(tree -> right, target);
	} else { //target == tree.val
		return True
	}
}
```
Of course, binary trees is often times not completely balanced, so without rebalancing mechanisms, there is a chance that the "tree" is more like a linked list, and searching becomes `O(n)`.




---
Categories: [[Data Structure]], [[CS50 - Introduction]]
References:
Created: 2024-06-13
