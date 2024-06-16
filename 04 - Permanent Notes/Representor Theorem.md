---
tags:
  - Statistics
  - "#NeedWork"
---
[[Reproducing Kernel Hilbert Space |RKHS]] in general is an infinite dimensional vector space.
Representor Theorem provides ways for us to be able to consider only a finite subspace of RKHS.

We are given a kernel $K$, a norm $||.||_H$ and inner product in the RKHS space $\langle . , . \rangle$, and we want to learn a linear function $f: H \to R$ 

All such functions have can be represented as:
$$
f(x) = \langle \omega, x \rangle_{H}
$$
for some normal vector $\omega \in H$.

consider a risk minimization problem of the form:
$$
minimize_{\omega \in H} R_{n}(\omega) + \lambda \Omega(||\omega||_{H})
$$

where the latter part of rhs is the regularizer.
For a given set $(X_i, Y_i)_{1...n} \in X, Y$ and a classifier $f$, let $R_n$ be the empirical risk of the classifier $l$ and $\Omega$ is a strictly monotonic increasing function. The Representor Theorem shows that the solution will always come in the form:
$$
w^* = \sum_{i=1}^n \alpha_{i}K(x_{i}, .)
$$
which can cut down dimensions all the way down to $R^n$ from infinity.

---
Categories: [[050-Statistics]]
References:
Created: 2024-05-01