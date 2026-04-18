# Multi-Layer Perceptrons

We define **layers** by some grouped units. Each unit here in graph is a neuron node. The input layer is the first layer, and the output layer is the last layer. The hidden layers are the layers between input and output layers. 

For a layer, if all input units are connected to all ouput units, then we call it a **fully-connected layer**. If such multilayer network consisting of fully-connected layers is called a **multilayer perceptron**.

Since each layer has a activation function, we can denote it as $f^{i}$ as the $i$-th layer. Then given a input $x$ the final result is $y = f^{L}(f^{L-1}(\cdots f^{2}(f^{1}(x))\cdots)) = f^{L}\circ f^{L-1}\circ \cdots \circ f^{2}\circ f^{1}(x)$.

## Activation Functions Among Layers

In intro part, we have talked about the limit of linear classification. Think what if we use linear activation function in each layer? Then we can get a linear model since the composition of linear functions is still linear. Actually, deep linear networks are no more expressive than linear regression, but it do have their uses and we will talk about it later.

If a neural nets is a directed acyclic graph (DAG), then it is called a **feed-forward neural network**. Multilayer feed-forward neural networks with nonlinear activation functions are **universal approximators**. That is, they can approximate any function arbitrary well.

We sometime perform logistic activation function where it can approximate a hard threshold function by scaling up the weights and biases. Furthermore, since logistic function is differentiable, we can use gradient descent to train the network.

One way to learn multilayer neural networks is to use [**backpropagation**](./Backpropagation).