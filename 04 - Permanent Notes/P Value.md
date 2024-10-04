---
tags:
---
# P Value
The formal (by formal I mean Wikipedia) definition of p value is as follows:

> The p value is the probability of obtaining test results as extreme as the result actually observed, under the assumption the null hypothesis is correct.

In other words, p value measures the "extremity" of a given observation. If an observation has a p value of 0.05, it means there's 5% chance it would've occurred under the [[Statistical Hypothesis|null hypothesis]].

## Definition
Consider an observed test statistic $t$ from an unknown distribution $T$. The p value $p$ is what the [[Prior Probability|prior probability]] would be of observing a statistic as extreme as $t$.
1. For right-tail test statistic distribution:
$$
p  = Pr(T>t | H_{0})
$$
2. For left-tail test statistic distribution:
$$
p = Pr(T < t | H_{0})
$$
3. For two-sided test statistic distribution:
$$
p = 2min(Pr(T > t | H_{0}), Pr(T < t|H_{0}))
$$

From the definitions above we can see a strong relation with p value and the [[Random Variable#^4367b7|cumulative distribution function]] of the test statistic, which becomes even clearer if we look at the visualization below:

![[p-value.jpg]]

## Uniform Distribution under H0
p values are uniformly distributed _if the null hypothesis is true_. Without loss of generality, consider the left-sided one-tailed hypothesis test. Let $F_t(t)$ be the function of test statistic under the null hypothesis, and let $t_{obs}$ be the observed test statistic.

The CDF of $p$ is:
$$
\begin{align} \\
F_{p}(P) &= Pr(P < p) \\
&= Pr(F_{t}(T) < p) \\
&= Pr(T < F^{-1}(p)) \\
&= F_{t}(F_{t}^{-1}(p)) \\
&= p
\end{align}
$$
Which is the CDF of the [[Uniform Distribution]] over the interval $[0,1]$. Therefore, p value is uniformly distributed if the null hypothesis is true.

## Distribution of p value
Now that we know that p values are uniformly distributed under null hypothesis, let's see how it's distributed when it's _not_, that is, if our new statistical hypothesis is true.
![[pvaluegraph.jpg]]
We can see that the distribution is heavily skewed towards the left (lower $p$). The interpretation is simple: if the Null Hypothesis were true, how do we have _THIS_ many seemingly "extreme" (low $p$) observations? The only explanation is that it is in fact, **NOT FROM THE NULL HYPOTHESIS DISTRIBUTION**. If the p value distribution looks more like the one in the right, it's a strong indicator that our statistical hypothesis may be correct.

---
Categories: [[050-Statistics]]
References:
https://www.simplypsychology.org/p-value.html
https://statproofbook.github.io/P/pval-h0.html
https://www.nonlinear.com/support/progenesis/comet/faq/v2.0/pq-values.aspx
