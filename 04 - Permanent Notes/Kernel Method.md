---
tags:
  - Statistics
---
Kernel Method in Machine Learning refers to a method that uses a "linear" classifier to solve a non-linear problem. the Kernel function will transform a given input data to a higher dimension, where it can be easily separated with a linear function.

Examples include:
- SVM
- Gaussian Kernel

### Kernel Trick
[![](https://upload.wikimedia.org/wikipedia/commons/thumb/c/cc/Kernel_trick_idea.svg/500px-Kernel_trick_idea.svg.png)](https://en.wikipedia.org/wiki/File:Kernel_trick_idea.svg)
let $\phi(x)$ be a transformation from Original feature space $X$ to $H$. For classification and other statistical tasks, one must know the inner product of two points: $\langle \phi(x), \phi(y) \rangle$ . This may take a long time to compute, so we  want a shortcut. This is where the Kernel Trick comes in.

A function $K: X \times X \to R$ is kernel if and only if there exists a Hilbert space H and a map $\phi: X \to H$ such that
$$
K(x, y) = \langle \phi(x), \phi(y) \rangle
$$
This means, we can just compute using the inputs and some kernel function $K$ and not explicitly using the transformation function. We can then view the kernel function as a function that measures "similarity" between two points in the feature map space.

## References

Created: 2024-05-01