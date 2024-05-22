---
tags:
  - DeepLearning
---
# Domain-Adaptive Neural Network

## Overview

- Deep Learning require a lot of data, which can often times be limited
- to overcome this problem, one can think of [[Deep Transfer Learning |transferring]] a model for Task A, which has a similar domain space, to another Task
- With the use of [[Maximum Mean Discrepancy]], we can optimize domain adaptation

## The Math

One can summarize the basic structure of Domain-adaptive Neural Network like so:
**Input > (Pretraining) > FC Layer > Out**
where pretraining can be done by Autoencoders, preferably DAE.
The Basic Structure is the same as your average NN, but with a twist in regularization - we use MMD to account for differences in domain. The loss function then, is as follows:
$$J_{DaNN} = J_{NNs} + \gamma MMD_e^2(q_s, \overline{q_t})$$
where:
$$J_{NNs} = -\frac{1}{n_s}\sum_{i=1}^{n_s}{\sum_{k=1}^{l}([y_s^i]_k log([f(x_s^i)]_k))}$$ 
is the loss function of typical NN and:
$$q_s = W_1^Tx_s + b, \overline q_t = W_1^Tx_t +b$$
are the linear combination of the outputs before activation.

Reminder that $J_{NNs}$ is for source data ONLY. We are using the knowledge of the source ($J_{NNs}$) with the discrepancy of the two different domains ($MMD_e^2(q_s, \overline q_t)$) in mind.

Minimizing the NN part of this function is easy, but for MMD, it depends on what [[Kernel Method]] we are using. Normally Gaussian Kernel is recommended as it's the most well-documented.

---
Categories: [[Deep Learning]]
Reference: 