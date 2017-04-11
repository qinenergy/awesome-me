# [dropout a simple way to prevent neural networks from overfitting](https://www.cs.toronto.edu/~hinton/absps/JMLRdropout.pdf)
## Introduction
1. Overfitting: stopping the training as soon as performance on a validation set starts to get worse, introducing weight penalties of various kinds such as L1 and L2 regularization and soft weight sharing.
2. Ideally: the best way to “regularize” a fixed-sized model is to average the predictions of all possible settings of the parametersits posterior probability given the training data, weighting its posterior probability given the training data
3. Dropout: It prevents overfitting and provides a way of approximately combining exponentially many different neural network architectures efficiently. So training a neural network with dropout can be seen as training a collection of 2n thinned networks with extensive weight sharing, where each thinned network gets trained very rarely, if at all.
4. The idea is to use a single neural net at test time without dropout. The weights of this network are scaled-down versions of the trained weights.
5. The idea of dropout is not limited to feed-forward neural nets. It can be more generally applied to graphical models such as Boltzmann Machines.
## Related work
1. Dropout can be interpreted as a way of regularizing a neural network by adding noise to its hidden units.
2. Dropping out 20% of the input units and 50% of the hidden units was often found to be optimal.
3. Since dropout can be seen as a stochastic regularization technique, it is natural to consider its deterministic counterpart which is obtained by marginalizing out the noise. I
4. In dropout, we minimize the loss function stochastically under a noise distribution. This can be seen as minimizing an expected loss function.
## Model
$$r ~ Bernoulli(p)$$
$$\hat{y} = r * y$$
## Learning
For each training case in a mini-batch, we sample a thinned network by dropping out units. The gradients for each parameter are averaged over the training cases in each mini-batch.
## Practical Guide
1. Network size: Therefore, if an n-sized layer is optimal for a standard neural net on any given task, a good dropout net should have at least n/p units.
2. Learning Rate and Momentum: A dropout net should typically use 10-100 times the learning rate that was optimal for a standard neural net. While momentum values of 0.9 are common for standard nets, with dropout we found that values around 0.95 to 0.99 work quite a lot better.
3. Max-norm Regularization: To prevent weights to grow very large, we can use max-norm regularization. This constrains the norm of the vector of incoming weights at each hidden unit to be bound by a constant c. Typical values of c range from 3 to 4. 
4. Dropout Rate: Typical values of p for hidden units are in the range 0.5 to 0.8. For real-valued inputs (image patches or speech frames), a typical value is 0.8. For hidden layers, the choice of p is coupled with the choice of number of hidden units n.
