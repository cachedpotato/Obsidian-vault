---
tags:
---
# Recurrent Neural Network
Recurrent Neural Network, or RNNs, is one of the most primitive _sequential data processing_ models. Advanced models such as [[Long Short-Term Memory|LSTM]] or [[Transformer]] are based on RNN. RNN is based on what's called a _recurrent unit_, which has 1) an input layer, 2) a hidden layer, and 3) output layer, just like any other feedforward neural networks.

## Structure
![[Pasted image 20250109121007.png|600]]

RNN is a function $f_{\theta}$ of type $(x_{t}, h_{t})\to(y_{t}, h_{t+1})$. the hidden layers $h$ serves as a _memory_ that tracks previous inputs.

RNNs have _tree types of weights_:
1) $W_{aa}$, which is for $h_t$ to $h_{t+1}$
2) $W_{ax}$, which is for input $x$ to hidden layer $h_t$
3) $W_{ya}$, which is for hidden layer $h_t$ to output $y$
![[Pasted image 20250109123156.png|300]]
Training is done via gradient descent, just like other neural network models. For each timestep $t$, the activation $a_t$ and the output $y_t$ are expressed as follows: 
$$
\begin{align}
a_{t} &= g_{1}(W_{aa}a_{t-1} + W_{ax}x_{t} + b_{a})  \\
y_{t} &= g_{2}(W_{ya}a_{t} + b_{y})
\end{align}
$$
One thing of note is that the recurrent neural network will backpropagate _through time_ during the training process. That is, it uses $t$ as the parameter:

$$
\frac{\partial\mathcal{L^{(T)}}}{\partial W} = \frac{\sum_{t}\partial\mathcal{L}^{(T)}}{\partial W}\Bigg|_{(t)}
$$

## Pros and Cons
As one would expect, RNN cannot escape from the vanishing gradient problem during the training process.

---
Categories: [[Deep Learning]], [[Machine Learning]]
References:
https://stanford.edu/~shervine/teaching/cs-230/cheatsheet-recurrent-neural-networks