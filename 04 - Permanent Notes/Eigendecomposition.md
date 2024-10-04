---
tags:
---
# Eigenvalue Decomposition
Before we delve into the decomposition part, we must know what eigenvalues/eigenvectors are.

Given an $n \times n$ matrix $A$, an _eigenvector_ of $A$ is a vector that satisfies the following:
$$
Av = \lambda v \qquad(\lambda \in \mathbb R)
$$
for some scalar $\lambda$. The $\lambda$ in this case is called the _eigenvalue_.

Geometrically speaking, this means that $A$ only elongates/shrinks along $v$ by the "scaling factor" of $\lambda$.

From the equation above, we get:
$$
\begin{align} \\
p(\lambda) &= \det(A - \lambda I) \\
& = \Pi_{i=1}^{N_{\lambda}}(\lambda - \lambda_{i})^{i}  \\
&= 0
\end{align}
$$

Where $N_{\lambda_i}$ is the number of eigenvalues.
For each eigenvalue $\lambda_i$, we have the eigenvalue equation
$$
(A - \lambda_{i}I)v = 0
$$

Now consider an $N \times N$ matrix $Q$ whose ith column is the eigenvector $q_i$ of $A$, and another $N \times N$ _diagonal_ matrix $\Lambda$ whose diagonal values are the corresponding eigenvalues ($\Lambda_{ii} = \lambda_{i}$). From the equations above,

$$
\begin{align}
Av &= \lambda v \\
AQ &= Q\Lambda \\
\therefore A &= Q\Lambda Q^{-1}
\end{align}
$$
This is called the **eigenvector decomposition**.

## Features of Eigendecomposition
- One of the more useful facts about decomposition is that the determinant of the original matrix $A$ is the same as the product of all its eigenvalues:
$$
\det(A) = \prod_{i=1}^{N_{\lambda}}\lambda_{i}^{n_{i}}
$$
- And also that the sum of eigenvalues is the same as the _trace_ of $A$:
$$
tr(A) = \sum_{i=1}^{N_{\lambda}}n_{i}\lambda_{i}
$$

- Because $\Lambda$ is a diagonal matrix, we can find the power series of $A$ much easier:
$$
\begin{align}
A^n &= A * A * \dots A \\
&= (Q\Lambda Q^{-1})^n \\
&= Q\Lambda(QQ^{-1})\Lambda(QQ^{-1})\dots(QQ^{-1})Q^{-1} \\
&= Q\Lambda^nQ^{-1}
\end{align}
$$
where
$$
\Lambda^n_{ii} = \lambda_{i}^n
$$

- $A$ is invertible if and only if all of its eigenvalues are nonzero.
## Geometrical Interpretation



---
Categories: [[050-Statistics]]
References:
