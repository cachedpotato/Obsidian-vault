---
tags:
  - DeepLearning
---
## Overview

Crux of DTL: **using the obtained knowledge from another task and dataset**
![[u9ue574z.bmp | 400]]
Advatnages
- reduce learning cost
- can work with limited amount of dataset
- the two tasks don't need to be strongly related for this to work

difference between [[semi-supervised-learning]]
- source and target datasets can have different distribution

DTL approaches
1. instance-based: AdaBoost/Dai etc. help utilize training instance from source domain
2. feature-based: minimize domain divergence by identifying good feature representation that can be used by both source and target domains
3. parameter-based: assumes models for related tasks share parameters or prior distribution of hyperparams. 
4. relational-based: Attempts to handle non IID data such as social network data.

## The Math
given a domain $D = \{X, P(X)\}$  where P is a [[marginal distribution]] of x,  a task T can be defined as:
$$ T = \{\Upsilon, P(Y|X)\} = \{\Upsilon,\eta \}, Y = \{y_1, ... , y_n\},  y_i \in \Upsilon $$
where
- $\Upsilon$  - Label space (Y is a sample of labels, $\Upsilon$ is the label space itself)
- $\eta$ - Predictive function, learned from $x$ ($y = \eta(x)$)

Given a source domain $D_s$ with a source task $T_s$ , DTL's purpose is to learn the target conditional probability distribution $P(Y_t | X_t)$ in $D_t$ where $D_s \neq D_t$ or $T_s \neq T_t$ .

source and target conditions can vary in four distinct ways:
- $X_s \neq X_t$ : feature space difference
- $P(X_s) \neq P(X_t)$ : probability distribution difference
- $\Upsilon_s \neq \Upsilon_t$ : Label space difference
- $P(Y_s|X_s) \neq P(Y_t | X_t)$ : conditional probability distribution difference 
## Categories and Types of DTL

Categories of DTL:
1. transductive
	similarities between tasks, but domains are different (only source labeled)
2. Inductive
	domains are the same, but tasks are different
3. Unsupervised
	similar to inductive transfer, with a focus on unsupervised tasks in target domain

Types of DTL:
- Domain adaptation: used normally when $P(X_s) \neq P(X_t)$ 
- Domain confusion: Nudge representations of both domains to be as similar as possible. See:  [[Domain-Adversarial Neural Network]] 
- Multitask Learning: Several tasks learned simultaneously
- One-shot Learning: Inferring required output based on a few training examples.
- Zero-shot Learning: No labeled examples to learn a task. This can be interpreted as learning three variables, $P(y | x, T)$ 

Reference: https://towardsdatascience.com/a-comprehensive-hands-on-guide-to-transfer-learning-with-real-world-applications-in-deep-learning-212bf3b2f27a

