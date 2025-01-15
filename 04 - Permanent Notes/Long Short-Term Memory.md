---
tags:
---
# Long Short-Term Memory
Long Short-Term Memory (LSTM) is a type of RNN that aims to provide a solution for the vanishing gradient problem the classic RNN has. Computationally, traditional RNNs are trained via backpropagation. As the model goes through more and more inputs, the long-term gradients (gradients for older inputs) can zero out.

LSTM fixes this by via an introduction of the "forget gate" - a module within the cell that decides whether to keep or forget the information. This can be useful for things such as grammatical dependencies.

## Structure
As mentioned above, the biggest feature of LSTMs are gates which decide whether or not to pass information forward - this is stored in a parameter called _cell state_, and it's dependent on gate outputs and previous cell states.
![[LSTM_Cell.svg.png|500]]
The image above shows a single cell of LSTM. $c_{t}$ above is the cell state, and it's computed using values from 4 distinct _layers_ that composes the 3 _gates_ of LSTM - the _forget gate_, the _input gate_, and the _output gate_, from left to right.

### 1. Forget Gate Layer
![[forget_gate.png]]

The Forget gate decides whether or not to _drop_ the previous cell. Gates are noted $\Gamma_{q}$  where q can be an arbitrary type of gate. For example, forget gates are often denoted as $\Gamma_{f}$. Gates are equal to:
$$
\Gamma_{q} = \sigma(W_{q}x_{t} + U_{q}h_{t-1} + b_{q})
$$
where $\sigma()$ is the sigmoid function, $W_{q}$ and $U_{q}$ are weight matrices for input/hidden layer, respectively, and $b$ is bias. $W$ and $U$ are sometimes denoted together as $W_q$.

Forget gate's activation vector, $f_t$ equates to
$$
\begin{align}
f_{t} = \Gamma_{f} &= \sigma(W_{f}x_{t} + U_{f}h_{t-1} + b_{f}) \\
&= \sigma(W_{f}[x_{t}, h_{t-1}] + b_{f})
\end{align}
$$

(The second line is just another representation of the formula above)
### Input Gate Layer
![[input_gate.png]]
This layer is actually 2 layers combined into one. First, we compute $i_t$, which decides how much of the selected information of the input to store.
$$
\begin{align}
i_{t} = \Gamma_{i} &= \sigma(W_{i}x_{t} + U_{i}h_{t-1} + b_{i}) \\
&= \sigma(W_{i}[x_{t}, h_{t-1} + b_{i}])
\end{align}
$$
Then we compute $\tilde{C_{t}}$, a _pseudo-cell-state_ that decides which information to store within the cell from current input.
$$
\begin{align} \\
\tilde{C_{t}} = \Gamma_{c} &= \tanh(W_{c}x_{t} + U_{c}h_{t-1}) + b_{c} \\
&= \tanh(W_{c}[x_{t}, h_{t-1}] + b_{c})
\end{align}
$$
To Summarize, $i_{t}$ is the _input gate's_ activation vector, whereas $\tilde{C_{t}}$ is the activation vector of the _cell input_.

### 3. Cell State Computation
![[cellstate 1.png]]
Our new cell state, $c_{t}$ is a _sum_ of two _Hadamard Products_:
1) Forget gate activation vector & previous cell state
2) Input gate activation vector & cell input activation vector
$$
C_{t} = C_{t-1} \odot f_{t} + i_{t} \odot \tilde{C_{t}}
$$
In Layman's terms, a Cell state $c_t$ is decided by
1) a _portion_ of the previous cell (can be nil)
2) a _portion_ of the new information


### 4. Output Layer
Now that we have our new cell state, all there's left is to compute the output and the hidden state vector.
![[output_gate.png]]

The output gate, just like any other gate, is computed like the following:
$$
\begin{align} \\
o_{t} = \Gamma_{o} &= \sigma(W_{o}x_{t} + U_{o}h_{t-1} + b_{o}) \\
&= \sigma(W_{o}[x_{t}, h_{t-1}] + b_{o}) 
\end{align}
$$
The output gate decides how much to reveal of the current cell. To compute the new hidden state, we compute the Hadamard product of the output activation vector and cell state with hyperbolic tangent as the activation function:
$$
h_{t} = o_{t} \odot \tanh(C_{t})
$$


---
Categories: [[Machine Learning]], [[Deep Learning]]
References:
https://dgkim5360.tistory.com/entry/understanding-long-short-term-memory-lstm-kr
https://en.wikipedia.org/wiki/Long_short-term_memory
https://stanford.edu/~shervine/teaching/cs-230/cheatsheet-recurrent-neural-networks
https://www.researchgate.net/publication/13853244_Long_Short-Term_Memory