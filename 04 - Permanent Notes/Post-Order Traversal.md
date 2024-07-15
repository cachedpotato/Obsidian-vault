---
tags:
---
# Post-Order Traversal
Unlike Pre-Order Traversal or In-Order Traversal, Post-Order Traversal checks the left and right daughter nodes first before traversing up to the parent node.
![[Pasted image 20240619201401.png|500]]
## The Code
```python
def Wrapper(root: Optional[TreeNode]) -> List[int]:
	res = []
	def postOrderTraversal(root: Optional[TreeNode]):
		if not root:
			return
		if root.left:
			postOrderTraversal(root.left)
		if root.right:
			postOrderTraversal(root.right)
		res.append(root.val)

	postOrderTraversal(root)
	return res
		
```

---
Categories: [[Traversal Algorithms]]
References:
