---
tags:
---
# Gamma-Poisson Distribution
The Gamma-Poisson Distribution, also known as the negative binomial distribution, is a probability distribution for _overdispersed_ count data. Overdispersion here means the presence of variability that cannot be explained just by the given statistical model. Given a Possion Distribution
$$
Pois(\lambda) = \frac{\lambda^ke^{-\lambda}}{k!}
$$
Because its variance, $\lambda$, is not independent of its mean which is the same, it therefore cannot be adjusted separately from the mean.
$$
Var(X) = E(X) = \lambda
$$
This can be troublesome for data that can have data within replicates (trials). For example, biological count data may seem apt for a normal [[Poisson Distribution]] - But more often than not this type of data vary more than what the Poisson distribution predicts. First let's look at how we'd model count data with replicate experiments using the Poisson distribution. let $n_i$ be number of fragments for gene $i$. Given a random sample of $r$ sequences from the entire library, the probability of a fragment being gene $i$ would be:
$$
\begin{align}
n &= n_{1} + n_{2} + \dots + n_{k}, \\
p_{i} &= n_{i} / n, \\
\lambda_{i} &= rp_{i}, \\
\end{align}
$$
If we were to use Poisson Distribution. There are two problems:
- For biological data, we are interested in comparing _between libraries_, not the statistics within a single dataset (control vs test).
- Due to difference in temperature, drug percentage (human error), etc., $p_i$ and $\lambda_i$ will vary even between replicates. This difference in variance _cannot be captured using Poisson Distribution_, because the formula is solely dependent on $p_i$.

Therefore, we need a new distribution model that can account for this overdispersion - this is where the Gamma-Poisson Distribution comes in. Gamma-Poisson Distribution is parameterized not only by its mean $\mu$ but also the overdispersion factor $\alpha$. This distribution is also known as the Negative Binomial Distribution, as it can also be used to model the number of _failures_ of a Bernoulli trial _before a given number of success occurs_.

Given number of success $k$, failure $r$, and probability of _success_ $p$,
$$
\begin{align}
f(k;r, p) = Pr(X=k) &= \binom{k + r - 1}{k}(1-p)^rp^k \\
&= \frac{\mathbb{\Gamma}(k + r)}{k!\mathbb{\Gamma}(r)}(1-p)^rp^k
\end{align}
$$
Where $\mathbb{\Gamma}(r)$ is the [[Gamma Function]]. This distribution has
$$
\begin{align}
\mu &= \frac{r(1-p)}{p} \\
\sigma^2 &= \frac{r(1-p)}{p^2}
\end{align}
$$

Reparametrizing this negative binomial function in terms with $\mu$ and $\alpha = 1/r$ gives the following:

$$
\begin{align}
f_{GP}(k;\mu,\alpha) = GP(\mu, \alpha) &= \frac{\mathbb{\Gamma}(k + 1 /\alpha)}{\mathbb{\Gamma}(k + 1)\mathbb{\Gamma}(r)}\left( \frac{\mu\alpha}{1 + \mu\alpha} \right)^k\left( \frac{1}{1 + \mu \alpha} \right)^{1/\alpha} \\
Exp(k) &= \mu \\
Var(k) &= \mu + \alpha \mu^2 \\
p &= \frac{\alpha \mu}{1 + \alpha \mu}
\end{align} 
$$

Here we can see the variance is not dependent on not just its mean but also the overdispersion factor $\alpha$. This will account for the biological noise present in replicates. if $\alpha$ is zero, this distribution will converge into Poisson Distribution.

Using the Gamma-Poisson Distribution, we can model our biological counts as follows:
$$
\begin{align}
Y^{treat}_{1}, Y^{treat}_{2},\dots Y^{treat}_{n_{1}} \sim GP(\mu_{treat}, \alpha) \\
Y^{control}_{1}, Y^{control}_{2},\dots Y^{control}_{n_{2}} \sim GP(\mu_{control}, \alpha)
\end{align}
$$








---
Categories: [[050-Statistics]], [[Probability Distribution]]
References:
