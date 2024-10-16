---
tags:
---
# Likelihood Function
In probabilistic modeling, we already know a good generative model for the randomness in the data. That is, we know the parameters to the probability function.
$$
F_{\theta} \to x \to P(x | \theta)
$$

Here we can compute the probability of observing $x$ for all possible instances of $x$ through deduction. However, in most experimental settings, we do not know the parameters. In fact, one of the primary focus of statistical analysis in most cases is finding the right distribution function and parameters of a given [[Random Variable|random variable]], given some sample set $X$. Therefore, we're trying to find the following function:
$$
\theta \to P(x | \theta) = \mathcal{L}(\theta|X)
$$
This is called the **likelihood function**. To be more exact, the likelihood function is a function that measures how well a statistical model explains observed data.

## Maximum Likelihood Function
Since we're trying to find the most optimal distribution that best explains the given sample set, we'd want our likelihood function, which measures the likeliness of the observed data, to output the _maximum_. The $\theta$ value that makes the observed data most likely, often noted as $\hat{\theta}$, is called _maximum likelihood estimator_. The steps are simple:
1) model the likelihood function $\mathcal{L}(\theta|X)$
2) find the $\theta$ value that maximizes this function. In other words, find the _global maxima_.

For example, say we have data points $x_{1}, x_{2}, \dots, x_{n}$ that we assume is from a Poisson distribution. The likelihood function then would be
$$
\begin{align} \\
\mathcal{L}(\theta|X) &= \prod_{i}Pois(x;\theta) \\
&= \prod_{i}\left( \frac{\lambda^{x_{i}}e^{-\lambda}}{x_{i}!} \right)
\end{align}
$$
This function in this form is rather hard to differentiate and find the global maxima. What we often do in this case is to apply logarithm. This is called the _log likelihood function_.
$$
\begin{align} \\
\log(\mathcal{L}(\theta|X)) &= \sum_{i}\log(Pois(x;\theta)) \\
&= \sum_{i}(-\theta + x_{i}\log(\theta) - \log(x_{i}!))
\end{align}
$$
To find the local maxima,
$$
\begin{align}
\frac{d\log(\mathcal{L}(\theta|X))}{d\theta} &= -n + \frac{\sum_{i}x_{i}}{\theta} = 0 \\
\hat{\theta} &= \frac{\sum_{i}x_{i}}{n} = \bar{X}

\end{align}
$$

Let's do another example with Binomial Distribution. Let $n$ be the number of trials and $k$ be the number of successes in our dataset.
$$
\begin{align} \\
\mathcal{L} (\theta|X) &= \binom{n}{k}p^k(1-p)^{n-k} \\
\log(\mathcal{L} (\theta|X)) &= \log(\binom{n}{k}p^k(1-p)^{n-k}) \\ \\
&= k\log c\theta + (n-k)\log(1-\theta), \quad c = \binom{n}{k} \\
\frac{d\log(\mathcal{L}(\theta|X))}{d\theta} &= \frac{k}{\theta} + \frac{k - n}{1 - \theta} = 0 \\
k\theta - k &= k\theta - n\theta \\
\therefore \hat{\theta} &= \frac{k}{n}
\end{align}
$$


---
Categories: [[Probability Theory]], [[050-Statistics]]
References:
