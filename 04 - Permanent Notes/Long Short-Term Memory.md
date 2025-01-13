---
tags:
---
# Long Short-Term Memory
Long Short-Term Memory (LSTM) is a type of RNN that aims to provide a solution for the vanishing gradient problem the classic RNN has. Computationally, traditional RNNs are trained via backpropagation. As the model goes through more and more inputs, the long-term gradients (gradients for older inputs) can zero out.

LSTM fixes this by via an introduction of the "forget gate" - a module within the cell that decides whether to keep or forget the information. This can be useful for things such as grammatical dependencies.

## Structure



---
Categories: [[Machine Learning]], [[Deep Learning]]
References:
https://dgkim5360.tistory.com/entry/understanding-long-short-term-memory-lstm-kr
https://en.wikipedia.org/wiki/Long_short-term_memory
https://stanford.edu/~shervine/teaching/cs-230/cheatsheet-recurrent-neural-networks