---
tags:
  - Statistics
---
Maximum Mean Discrepancy is a [[Kernel Method| Kernel]] based statistical test for calculating the difference between two statistical distribution. To be more specific, it's a difference between feature means.

Let X and Y be samples of distributions p and q, respectively. How can we tell X and Y come from different distributions? In fact, how can we tell how different p and q are from each other?

One way of doing this can be measuring the difference in sample mean:
$$
E_{x}[X] - E_{y}[Y]
$$
Which can work in some cases, but we can easily think of two different distributions with the same mean. Clearly, using the mean isn't enough. Then is using variance enough? What about other higher orders? It seems like to accurately measure the difference between the two, we need to take into account infinite amount of orders. How can we do this?

By transforming the input space into a higher dimension of course. To be more specific, a [[Reproducing Kernel Hilbert Space]] will do just that. Think of a transformation $\phi$ that transforms x to $\phi(x)$ which resides in RKHS H. measuring the difference here will be a more accurate depiction of differences between two distributions:
$$
MMD := \sup_{f\in F}(E_{x}[\phi(x)] - E_{y}[\phi(y)])
$$
Because this is RKHS, we can use the reproducing kernel K in such a way that

$$
\begin{flalign}
MMD^2[F, p, q] & =  [sup_{||f||_{H}\leq_{1}}[E_{x}[f(x)]-E_{y}[f(y)]]^2 \\
& = [sup_{||f||_{H}\leq_{1}}\langle\mu_{p}-\mu_{q}, f\rangle_{H}]^2 \\
& = ||\mu_{p} - \mu_{q}||_{H}^2 \\
& = E_{x,x'}[k(x,x')] -2E_{x,y}[k(x,y)]+E_{y,y'}[k(y,y')] \\
& = \frac{1}{m^2}\sum_{i=1}^m\sum _{j\neq i}^mk(x_{i}, x_{j}) + \frac{1}{n^2}\sum_{i=1}^n\sum _{j\neq i}^nk(x_{i}, x_{j}) - \frac{2}{mn}\sum_{i=1}^m\sum _{j=1}^nk(x_{i}, y_{j}) \\
\end{flalign}
$$

where $[K_{ab}]_{ij}$ is the Gram matrix, and $Tr()$ is a trace function.

It is also important to note that the mean $\mu_x$ itself is called a mean embedding, and in RHKS, this is actually the probability distribution p! Which makes sense, since this whole time we were trying to find, essentially, $||p-q||_{H}$ .


## References
https://jmlr.csail.mit.edu/papers/v13/gretton12a.html

Created: 2024-05-01