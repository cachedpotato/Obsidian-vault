---
tags:
  - "#Statistics"
  - NeedWork
---
Reproducing Kernel Hilbert Space (RHKS) is a [[Hilbert Space]] of functions where point evaluation is linear functional. In layman's terms, if $||f - g||$ is small, then $f(x)$ must be close to $g(x)$

By definition of kernels, we can easily see that given input space $X$ and Hilbert space $H$, there exists a kernel $K$ such that
$K(\phi(x), \phi(y))$

What about the other way? In other words, given input space X and function $K$, is there a Hilbert Space $H$ such that the function K is the kernel function?

If such property holds, this Hilbert Space $H$ is called the Reproducing Kernel Hilbert Space (RKHS).

### Rather informal proof
consider a mapping $\phi: X \to R^X$ where $R^X$ is a space of all function that maps $X \to R$. then, we can define feature mapping
$$
x \to \phi(x):= k_{x} := k\langle x, .\rangle
$$
We can see that our input x is mapped as a function in space $H$. That's because Hilbert space here is a space of functions. here, $x$ is not an argument, rather it's the **parameter**
$$
k_{x}: X \to R, \quad x\in X, \quad k_{x}(y) = k(x, y)
$$
Now consider a collection of "images" of mapping of x. Using this, we can create a span $G$ as a linear sum of all image vectors:
$$
G: \{\sum_{i=1}^n\alpha_{i}k\langle x_{i}, .\rangle | \alpha_{i} \in R, n \in N, x \in X\}
$$
For G to be a Hilbert Space, we need to define a scalar product.
let $f: \sum_{i=1}^n\alpha_{i} k\langle x, .\rangle$ and $g: \sum_{j=1}^m\beta_{i} k\langle y, .\rangle$
then, the scalar product is:
$$
\begin{flalign}
\langle f, g\rangle_{G} & = \left\langle  \sum_{i=1}^n\alpha_{i} k\langle x_{i}, .\rangle, \sum_{j=1}^m\beta_{i} k\langle y_{j}, .\rangle  \right\rangle \\
& = \sum_{i=1}^m \sum_{j=1}^n \alpha_{i} \beta_{j}k\langle x_{i}, y_{j} \rangle
\end{flalign}
$$

The only way for this to be a scalar product, the function $k$ _must_ be a kernel function we have defined above. By construction, k has the following property: 
$$
k(x, y) = \langle \phi(x), \phi(y)\rangle
$$

What's neat about the Reproducing Kernel Hilbert Space, is that has the reproducing quality:
$$
\begin{flalign}
\langle f, k\langle x, .\rangle \rangle & = \left\langle  \sum_{i=1}^n\alpha_{i} k\langle x_{i}, .\rangle, k\langle x, ,\rangle  \right\rangle \\
 & = \langle \sum_{j=1}^m\alpha_{i} k\langle x_{i}, x \rangle \rangle \\
 & = f(x)
\end{flalign}
$$
We can see that f(x) is the inner product of $f$ and $k\langle x, . \rangle$. Remember that the latter term is the **image of the input point**. this means we can **reproduce** $f(x)$ in RKHS by getting the inner product of the image and the function.

### A more formal proof
Let X be an arbitrary set and H be a Hilbert Space on X. The evaluation functional is a function that evaluates at point x:
$$
L_{x}: f \to f(x) \quad \forall f \in H
$$

$H$ is RHKS if $L_x$ is continuous for all x in X and for all f in H.
This can be re-written as:
$$
\forall f\in H \quad \exists M_{x}\geq_{0}\quad s.t.\quad|L_{x}(f)| := |f(x)| \leq M_{x}||f||_{H}
$$
This assures the inner product and evaluation of every function in H remain in the domain. This also guarantees the evaluation function can be interpreted as an inner product of f and some other function $K_x$, implying there exists a unique element $K_x$ which has a 'reproducing property':
$$
f(x) = L_{x}(f) = \langle f, K_{x}\rangle_{H} \quad\forall f \in H
$$

since $K_x$ is also a function of X,
$$
K_{x} = L_{y}(K_{x}) = \langle K_{x}, K_{y}\rangle\quad where\quad K_{y} \in H
$$
We can then define the reproducing kernel $K: X \times X \to R$:
$$
\begin{flalign}
K(x, y) & = \langle K_{x}, K_{y}\rangle_{H} \\
& = \langle K(x, .), K(y, .)\rangle_{H}
\end{flalign}
$$
Note that $K(x, .)$ takes x as **parameter** not a variable

---
Categories: [[Statistics]]
References:
https://www.youtube.com/watch?v=EoM_DF3VAO8
Created: 2024-05-01