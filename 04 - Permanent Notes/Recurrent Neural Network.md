---
tags:
---
# Recurrent Neural Network
Recurrent Neural Network, or RNNs, is one of the most primitive _sequential data processing_ models. Advanced models such as [[Long Short-Term Memory|LSTM]] or [[Transformer]] are based on RNN. RNN is based on what's called a _recurrent unit_, which has 1) an input layer, 2) a hidden layer, and 3) output layer, just like any other feedforward neural networks.

## Structure
![[Pasted image 20250109121007.png|600]]

RNN is a function $f_{\theta}$ of type $(x_{t}, h_{t})\to(y_{t}, h_{t+1})$. the hidden layers $h$ serves as a _memory_ that tracks previous inputs.

RNNs have _tree types of weights_:
1) $W$, which is for $h_t$ to $h_{t+1}$
2) $U$, which is for input $x$ to hidden layer $h_t$
3) $V$, which is for hidden layer $h_t$ to output $o$
![[Pasted image 20250113112802.png]]
Training is done via gradient descent, just like other neural network models. For each timestep $t$, the activation $a_t$ and the output $y_t$ are expressed as follows: 
$$
\begin{align}
h_{t} &= g_{1}(Ux_{t} + Wh_{t-1} + b)  \\
y_{t} &= g_{2}(Vh_{t} + c)
\end{align}
$$

$g_1$ and $g_2$ are activation functions, the selections of which are often [[Rectified Linear Unit|ReLU]]/tanh and softmax, respectively.

It's important to note that  the weight matrices are shared _temporally_. On any given $t$, the operation will be done on the same shared weight matrix.

To visualize, the RNN looks something like this:
![[Pasted image 20250113114609.png|600]]
## Training
The recurrent neural network will backpropagate _through time_ during the training process. That is, it uses $t$ as the parameter:

$$
\frac{\partial\mathcal{L^{(T)}}}{\partial W} = \frac{\sum_{t}\partial\mathcal{L}^{(T)}}{\partial W}\Bigg|_{(t)}
$$

To visualize, gradient will run through the hidden state in the direction of the _red arrow_ below:
![[Pasted image 20250113115008.png|400]]

## Pros and Cons
As one would expect, RNN cannot escape from the vanishing gradient problem during the training process.

---
Categories: [[Deep Learning]], [[Machine Learning]]
References:
https://stanford.edu/~shervine/teaching/cs-230/cheatsheet-recurrent-neural-networks
https://towardsdatascience.com/recurrent-neural-networks-rnns-3f06d7653a85