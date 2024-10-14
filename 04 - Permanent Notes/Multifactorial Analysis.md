---
tags:
---
# Multifactorial Analysis
Let's say we want to figure out the degree of influence something has on the expression levels of genes. For example. Along with siRNA knockdown, we also want to test out the effect of some drug. Since we're trying to measure _multiple factors_' effect on result, this is called **multifactorial analysis**. 

Let $y$ be the expression level, $x_{1}$ be the first factor - siRNA knockdown and $x_2$ be the second factor - the effects of the drug. Then, we can write the gene expression notation as follows:
$$
y = \beta_{0} + x_{1}\beta_{1} + x_{2}\beta_{2} + x_{1}x_{2}\beta_{12}
$$
$x_i$ are the _factors_, and are binary - either the factor is "active" (1) or "inactive" (0). A matrix of all possible combination of factors is called the _design matrix_. $\beta_{i}$ are the _coefficients_ of said factors. $\beta_{0}$ represents the base level of measurement in negative control (where all factors are not active), and is called the _intercept_.

Along with factors $x_{1}$ and $x_2$, we also have $x_{12}$. This is yet another factor that we didn't explicitly specify, but represents the _interaction between two factors $x_{1}$ and $x_{2}$_. 
$$
\begin{align}
y = \beta_{0} + \beta_{1} + \beta_{2} + \beta_{12}  \\
\beta_{12} = y - (\beta_0 + \beta_{1} + \beta_{2})
\end{align}
$$
In other words, $\beta_{12}$ explains the difference between actual expression and the sum of influence of individual factors (+ baseline).

To generalize for measurement of interest $y_{j}$, given the number of factors $k$,
$$
y_{j} = \sum_{k}x_{jk}\beta_{k}
$$

## Addressing Noise
Of course because of biological noise that happens between replicates (and other unexplainable variances), the expression level will not perfectly match with the sum of factors and coefficients. Therefore, we need to add another term $\epsilon_{j}$ to the mix to address the noise. $\epsilon_{j}$ is often referred to as the residual.
$$
y_{j} = \sum_{k}x_{jk}\beta_{k} + \epsilon_{j}
$$
Of course, we do not want the _residual_ to explain most of the expression levels - we want the value to be as low as possible. That is, we need a way to minimize the residual. One common way is to minimize the sum of squares. This is the commonly known **Least Sum of Squares Error**.
$$
\sum_{j}\epsilon_{j}^2 \quad \to \quad \min.
$$
The problem with this approach is that it is sensitive to outliers, and therefore not [[Robustness|robust]]. Few other minimization methods are used to address this problem, including:
$$
\begin{align} \\
R &= \sum_{j}|\epsilon_{j}|\\
R &= \sum_{j}\rho_{s}(\epsilon_{j}) \\
R &= \sum_{j}Q_{\theta}(\{\epsilon_{1}^2, \epsilon_{2}^2,\dots,\epsilon_{n}^2\}) \\
R &= \sum_{j}w_{j}e_{j}^2 \\
\end{align}
$$
- Least Absolute Deviations: generalization of median, which is considered more robust than average.
- M-Estimation: Uses a _penalization function_ $\rho_{s}$ that is quadratic if $|\epsilon| < s$ and flattens out afterwards.
- LTS, QTS: Sum of squares but in different quantiles (50%, 90%)
- Weighted Regression: adds weight $w_{j}$ to weight down outliers.

## Effects of Multifactorial Analysis
This may seem counterintuitive, but multifactorial analysis, which takes into account more factors for measurement and thus seem as a "stricter" form of measurement, can lead to an _increase of stronger p value samples_. This is because if we only use one factor, the variability has to be absorbed by the residuals ($\epsilon$). This leads to higher levels of noise and uncertainty in $\beta$-estimates. 

On the other hand, taking more factors into account means more parameters need to be estimated, and thus can lead to decrease in [[Degrees of Freedom|degrees of freedom]]. The effects of noise and degrees of freedoms are _counteracting_, so one can't say for certain if increasing factors will lead to stronger results.


---
Categories: [[050-Statistics]], [[Bioinformatics]]
References:
