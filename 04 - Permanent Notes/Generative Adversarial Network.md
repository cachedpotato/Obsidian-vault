---
tags:
---
# Generative Adversarial Network
Generative Adversarial Network, or GAN for short, is a machine learning framework for [[Generative Artificial Intelligence]], where two neural networks contest each other in the form of a zero-sum game. 

Say we have two Neural Networks: A and B. A and B plays a "game" where:
- A, the "counterfeiter", aims to create counterfeits that are undetected by B
- B, the "police", aims to accurately distinguish real (actual data) from the counterfeits (perturbed data by A).
The network is then trained until theoretically, A produces perfect counterfeits and B is able to perfectly tell apart real from fake. Essentially Both networks are training to hone their respective skill to win against the other.

![[Pasted image 20241129165914.png]]


# The Math
### 1. Variables / Distributions
- $x$: our data (random variable)
- $p_g$: the generator's distribution over data $x$
- $z$: our noise variable
- $p_z(z)$: prior probability of noise variable $z$
- $G(z; \theta_{g})$: Generator Network, a.k.a the "counterfeiters"
- $D(x; \theta_{d})$: Discriminator Network, a.k.a the "police"
	- Represents probability that $x$ came from data rather than $p_g$

### 2. Value Function and the minimax game
To train GAN, we need to train both the generator $G$ and discriminator $D$. For the discriminator, this means we want to maximize the probability of assigning correct labels to both real and generated data. In other words, we want to maximize the expected value of $D(x)$ for real data points $x$.
$$
\max_{D}V(D) = \mathbb{E}_{x \sim p_{data}(x)}[\log D(x)]
$$
For the Discriminator, we want to do the opposite: we want the discriminator to assign incorrect labels for the generated data $G(z)$:
$$
\min_{G}V(G) = \mathbb{E}_{z \sim p_{z}(z)}[\log(1 - D(G(z)))]
$$
If the Discriminator $D$ falsely assigns the counterfeited data $G(z)$ as real data (close to 1), the value of $(1-D(G(z)))$ will decrease to 0. 
Since we're training both $D$ and $G$ together, the final value function $V(D, G)$ and our objective "minimax game" is:
$$
\min_{G}\max_{D}V(D, G) =\mathbb{E}_{x \sim p_{data}(x)}[\log D(x)] +\mathbb{E}_{z \sim p_{z}(z)}[\log(1 - D(G(z)))] 
$$
### 3. Optimal Discriminator
$$
\begin{align} \\
V(G, D) &= \int_{x}p_{data}(x)\log(D(x))dx + \int_{z}p_{z}(z)\log(1-D(G(z)))dz  \\
&= \int_{x}p_{data}(x)\log(D(x))dx + \int_{x}p_{g}(x)\log(1-D(x))dx \\
&=\int_{x}p_{data}(x)\log(D(x)) + p_{g}(x)\log(1-D(x))dx 
\end{align}
$$

Our goal is to get the maximum value of V. For this, we need the term inside the integral to be it's optimum. For any $(a, b) \in \mathbb{R}^2$ , the function $a\log(y) + b\log(1 - y)$ reaches its maximum at $a/b+a$. therefore, the optimal Discriminator is
$$
D^*_{G}(x) = \frac{p_{data}(x)}{p_{data}(x) + p_{g}(x)}
$$

### 4. Global minimum of training criterion C(G)
Now that we found the optimal discriminator, now it's time to find the optimal generator. By intuition, we can see that the best generator will be the one generating data that is **identical** to the real data, that is,
$$
p_{data}(x) = p_{g}(x)
$$
This essentially makes the generator a random coin flip:
$$
\begin{align}
D^*_{G}(x) &= \frac{p_{data}(x)}{p_{data}(x) + p_{g}(x)} \\
&= \frac{p_{data}(x)}{p_{data}(x) + p_{data}(x)}  \\
&= \frac{1}{2}
\end{align}
$$

Now let's see if this is actually the case. First, let's assume we have $p_g$ identical to $p_{data}$. Then,
$$
\begin{align}
C(G) = \max V(G,D) &= \int p_{data}\log\left( \frac{1}{2} \right) +p_{g}\log\left( 1 -\frac{1}{2} \right) dx \\
&= -\log(2)\int p_{data}dx  -\log(2)\int p_{g}(x)dx \\
&= -2\log(2)
\end{align}
$$

Rearranging the Value Function equation (extracting $-\log4$) gives:
$$
\begin{align} \\
C(G) &=\int_{x}p_{data}(x)\log(D(x)) + p_{g}(x)\log(1-D(x))dx  \\
&= \int_{x}p_{data}(x)\log\left( \frac{p_{data}(x)}{p_{data}(x) + p_{g}(x)} \right)+ p_{g}(x)\log\left( \frac{p_{g}(x)}{p_{data}(x) + p_{g}(x)} \right)dx  \\
&= \int_{x}p_{data}(x)(\log\left( p_{data}(x)-\log\left( \frac{{p_{data}(x) + p_{g}(x)}}{2}  \right)-\log(2) \right) + p_{data}(x)(\log\left( p_{g}(x)-\log\left( \frac{{p_{data}(x) + p_{g}(x)}}{2} \right)-\log(2) \right)  \\
&= -2\log(2) + \int_{x}p_{data}(x)\left( p_{data}(x) - \log\left( \frac{{p_{data}(x) + p_{g}(x)}}{2} \right) \right)dx + \int_{x}p_{g}(x)\left( p_{g}(x) - \log\left( \frac{{p_{data}(x) + p_{g}(x)}}{2} \right) \right)dx \\
&=-\log(4) + D_{KL}\left( p_{data}(x) || \log\frac{{p_{data}(x) + p_{g}(x)}}{2} \right) + D_{KL}\left( p_{g}(x) || \log\frac{{p_{g}(x) + p_{g}(x)}}{2} \right)  \\ \\
\because D_{KL}(P||Q) &= \sum P(x)\log\left( \frac{P(x)}{Q(x)} \right)
\end{align}
$$

The final two terms make up what's called the Jensen-Shannon Divergence, which is, in layman's terms, the "distance-ification" of [[Kullback-Leibler Divergence]], which is _not_ symmetrical. 
$$
J(P, Q) = \frac{1}{2}(D_{KL}(P||R) + D_{KL}(Q||R)) \quad where \quad R= \frac{{P+Q}}{2}
$$
Therefore, the final expression for $C(G)$ becomes:
$$
\begin{align} \\
C(G) &= \mathbb{E}_{x \sim p_{data}(x)}[\log D(x)] +\mathbb{E}_{z \sim p_{z}(z)}[\log(1 - D(G(z)))]\\
&=\int_{x}p_{data}(x)\log(D(x)) + p_{g}(x)\log(1-D(x))dx  \\
&= -\log(4) + D_{KL}\left( p_{data}(x) || \log\frac{{p_{data}(x) + p_{g}(x)}}{2} \right) + D_{KL}\left( p_{g}(x) || \log\frac{{p_{g}(x) + p_{g}(x)}}{2} \right) \\
&= -\log(4) + 2J(p_{data}(x), p_{g}(x))
\end{align}
$$

The Discriminator's goal is to **minimize** the value function. Since the Jensen-Shannon Divergence is a distance metric, it can't go below zero, and it's minimum is zero if and only if $p_{data}(x) = p_{g}(x)$, proving our intuition.

### 5. Visual representation
![[스크린샷 2024-12-26 155222.png]]
The Discriminator is the blue line and the generator is the green line. As the model get's trained, the generator becomes more and more similar to the real data's distribution (black dotted line), and the discriminator, once being a somewhat competent logarithmic classifier, converges to a coefficient $\frac{1}{2}$ , essentially being unable to tell apart the real data from the fake.

## Pros and Cons of GAN
GAN is a powerful generative model that laid the groundwork for modern generative artificial intelligence. GAN is powerful in that it does not need [[Markov Chains]] or [[Backpropagation]] during the training process. However, GAN still has some glaring weaknesses.

### 1. Mode Collapse
This is when GAN fails to generalize properly due to the generator finding a sample that the discriminator can't distinguish accurately early on during the training process, and generating only samples that match the low-accuracy samples only. the _Helvetica Scenario_ is an infamous example of this, where the generator only generated images of 0.

### 2. Vanishing Gradient
Contrary to the mode collapse, if the discriminator learns too fast compared to the generator, the model cannot further lower its loss function and the gradient converges to zero. 


---
Categories: [[Machine Learning]], [[Generative Artificial Intelligence]]
References:
https://arxiv.org/abs/1406.2661
https://en.wikipedia.org/wiki/Generative_adversarial_network