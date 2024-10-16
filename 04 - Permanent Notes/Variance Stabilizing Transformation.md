---
tags:
---
# Variance Stabilizing Transformation
Empirical measurements are different from theoretical replicates in that the replicates are in fact, not exactly the same. This means in an experimental setting, it's harder for us to know if the difference in observation is a true/significant difference between conditions or just biological noise. 

## Heteroskedasticity
Heteroskedasticity means the variance of errors is not constant across observations. In other words, the variance of our data is different in different regions of our data space. For example, the variance may increase along one axis with the mean.
![[heteroskedasticity1-1024x390.webp]]
This is troublesome for regression tasks, as regression normally assume _homoskedasticity_ - the variance remains the same through our data space.

To mitigate this problem, we need some sort of preprocessing to our data to make the variance consistent. This is called **variance stabilizing transformation**.

## Applying VST with delta method
Transformations are essentially functions we apply to our [[Random Variable|random variables]]. What functions to apply will differ based on the variable's distribution, but they can be figured out using the _delta method_.

Let $g$ be our differentiable transformation function. This function must assure the variance stays consistent within our data space of random variables $X_{i}$, with means $\mu_{i}$ variances $v_{i}$. Assume means and variances are related by a functional relationship $v_{i} = v(\mu _{i})$.

For values of $X_i$ in the neighbor of its means $\mu_{i}$,
$$
g(X_{i}) = g(\mu_{i}) + g'(\mu_{i})(X_{i} - \mu_{i}) + \dots
$$
We will be ignoring higher order terms as they're insignificant. For the variance of the transformed variable to be constant,
$$
\begin{align}
Var(g(X_{i})) &= Var(g(\mu_{i}) + g'(\mu_{i})(X_{i} - \mu_{i})) \\
&= Var(g'(\mu_{i}) (X_{i}-\mu_{i})) \\
&= Var(g'(\mu_{i})X_{i} - \mu_{i}g'(\mu_{i})) \\
&= g'(\mu_{i})^2Var(X_{i}) \\
&= g'(\mu_{i})^2v(\mu_{i}) = C,\quad C \in \mathbb{R}\\
\therefore g'(\mu_{i}) &= \frac{1}{\sqrt{ v(\mu_{i}) }} \\
g'(x) &= \frac{1}{\sqrt{ v(x) }} \\
g(x) &= \int g'(x)dx = \int \frac{1}{\sqrt{ v(x) }}dx
\end{align}
$$

## Example VST
Let's use the equation above to find the appropriate transformations for various distributions.
1) Poisson distribution
$$
\begin{align}
v(\mu) &= \mu \\
g(x) &= \int \frac{1}{\sqrt{ v(x) }}dx \\
&=\int \frac{1}{\sqrt{ x }}dx \\
&= 2\sqrt{ x } + C
\end{align}
$$
since the integral constant and the coefficient is not of interest, we only need to apply square root to our variable for the transformation.

2) Quadratic relationship with the mean
$$
\begin{align}
v(\mu) &= \alpha \mu^2 \\
g(x) &= \int \frac{1}{\sqrt{ v(x) }}dx \\
&=\int \frac{1}{x}dx \\
&= \ln(x) + C
\end{align}
$$
This explains why logarithm transformation is used so frequently in data analysis. It acts as a variance stabilizing mechanism whenever the standard deviation is proportional to the mean.

3) [[Gamma-Poisson Distribution]]
$$
\begin{align}
v(\mu) &= \mu + \alpha \mu^2 \\
g(x) &= \int \frac{1}{\sqrt{ x + \alpha x^2 }}dx \\
&= \frac{1}{\sqrt{ \alpha }}\ln(2\sqrt{ \alpha(\alpha x^2 + x) } + 2\alpha x + 1) \\
&= \frac{1}{2\sqrt{ \alpha }}arcosh(2\alpha x+1)
\end{align}
$$
This stabilizing function has interesting properties:
* if $x$ is near zero, the stabilizing function behaves like a square root function, which is the same with Poisson distribution.
* if $x$ is large and $\alpha > 0$, the function behaves like a logarithm.

Looking at the variance of the Gamma-Poisson Distribution, we can get an intuitive explanation:

For lower values of $x$, the noise is insignificant enough to assume the variable follows a Poisson distribution, whereas for higher values of x the overdispersion effect takes over and much of the variance is explained by noise.


---
Categories: [[050-Statistics]], [[Bioinformatics]]
References:
https://corporatefinanceinstitute.com/resources/data-science/heteroskedasticity/
