---
tags:
---
# Traversal Algorithms
There are TONS of Algorithms for traversing a tree or a graph. Think of this as the "main hub" for traversal algorithm notes



## Order Traversals
Here we'll talk about order-traversal algorithms, which is a term I just made up to group these three algorithms:
- [[In-Order Traversal]]
- [[Pre-Order Traversal]]
- [[Post-Order Traversal]]

The differences among these algorithms will be explained below, but one thing in common is that these all use [[Depth First Search Algorithm]].

### Creating a Binary Tree from Order-Traversal lists
if given two lists in either:
- In-Order Traversal and Pre-Order Traversal
- In-Order Traversal and Post-Order Traversal
We can construct a valid Binary Tree.

1) Preorder and Inorder
- Preorder's first is always the root
- Find where preorder's first is located in in order (split).

- in order left from split: left subtree
- in order right from split: right subtree
- pre order from index root + 1 to root + split: left subtree
- pre order index root + split + 1: root of new subtree
```python
def constructBinaryTree(inorder: List[int], preorder: List[int]) -> Optional[TreeNode]:
	if not inorder or not preorder:
		return None

	root = preorder[0]
	split = inorder.index[preorder[0]]
	root.left = constructBinaryTree(
		inorder[ : split], preorder[1 : split + 1]
	)
	root.right = constructBinaryTree(
		inorder[split+1 : ], preorder[split+1 : ]
	)

	return root
```

---
Categories: [[Computer Algorithms]]
References:
