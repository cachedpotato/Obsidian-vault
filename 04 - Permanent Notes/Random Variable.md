---
tags:
---
# Random Variable
A random variable is a mathematical _function_ in which
- The **domain** is the set of possible outcomes in a _sample space_
- the **range** is a measurable space, often real-number set.

To be more precise, a random variable $X$ is a measurable function $X: \Omega \to E$ where $\Omega$ is the sample space of the probability triple. The probability triple are:
- Sample space $\Omega$
- Event space $\mathcal{F}$ (set of outcomes from sample space)
- Probability Function $P$
The probability function $P(X)$ that $X$ takes on a value in a measurable set $S \subseteq E$ is:
$$
P(X \in S ) = P(\{\omega \in \Omega|X(\omega) \in S\})
$$
![[Pasted image 20240930144647.png]]

There are two types of random variables.
1. Discrete random variable: $X$ can only take some values. For example, number of heads from 3 coin flips can only be 0, 1, 2 or 3.
2. Continuous random variable: $X$ can take any value from a continuous range. For example, an average person's height can take any value from around 150 to 200.

## Functions of Random Variable

^4367b7

As can be seen from the image above, Given a random variable $X$ defined by probability triple $(\Omega, \mathcal F, P)$, we can ask question such as "What is the probability of X being 3?". This can be written in a multitude of ways:
- $P(\{\omega \in \Omega | X(\omega) = 2\})$
- $\{\omega: X(\omega) =  2\}$
- $P(X = 2)$
- $p_X(2)$
The latter two is used most frequently. Record all probabilities of possible outputs of $X$ gives us the _probability distribution function_. 
Notice how the latter two does not have any sort of annotation for the sample space. In a way, we're _forgetting_ the underlying sample space and trying to look at the connection between random variable X _straight to the measurable space_ $S$. 

The probability that $X$ will take less or equal to some value $x$ is called the **Cumulative Distribution Function**, and is interchangeable with the Probability distribution function. 
$$
F_{X}(X) = P(X \leq x) 
$$
CDF has these properties:
- CDF is right-continuous, monotone increasing function
- It has the range of $[0,1]$: $F: \mathbb{R} -> [0,1]$
- Differentiating the CDF will give the [[Probability Density Function and Probability Mass Function|probability density function]] for continuous random variable, and probability mass function for discrete variable.
$$
f(x) = \frac{F(x)}{dx}
$$
- The CDF then, can be written as the integral of $f$:
$$
F(x) = \int^x_{-\infty}f(x)dx
$$

---
Categories: [[Probability Theory]], [[050-Statistics]]
References:
