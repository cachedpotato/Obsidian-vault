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
Let's define some variables:
- $x$: our data (random variable)
- $p_g$: the generator's distribution
- $z$: our noise variable
- $p_z(z)$: prior probability of noise variable $z$
- $G(z; \theta_{g})$: Generator Network, a.k.a the "counterfeiters"
- $D(x; \theta_{d})$: Discriminator Network, a.k.a the "police"





---
Categories: [[Machine Learning]], [[Reinforcement Learning]]
References:
https://arxiv.org/abs/1406.2661
https://en.wikipedia.org/wiki/Generative_adversarial_network