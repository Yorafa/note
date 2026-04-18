## Introduction to Neural Networks

In previous ML/SL courses, we learned many classification and regression algorithms. However, these algorithms are not very good at dealing with complex data. For example, in the image recognition problem, we need to extract features from the image, and then use these features to train a classifier. However, the feature extraction process is very time-consuming and difficult. In this course, we will learn a new type of machine learning algorithm, called neural networks, which can automatically extract features from the data.

Beyond that, we would like to talk more about the limit about the linear classification.

## Limit of Linear Classification

One of the most important property that linear classification needed is linear separability. To analyze if a dataset is linear separable, we want to introduce the concept of convex set.

### Convex Set

A set $S$ is convex if for any two points $x, y \in S$, the line segment between $x$ and $y$ is entirely contained in $S$. Mathematically, we can write it as: $\forall x,y \in S \implies \lambda x + (1 - \lambda)y \in S, \forall \lambda \in [0, 1]$

Now, to prove a set is linear separable, we can prove that the set is convex.

If we can not find a linear separable dataset, then we can not use linear classification to solve the problem. Sometimes, we may have some ways to transform the dataset to make it linear separable. However, this is not always possible and may not be efficient (hard to pick good basis functions, etc.).

Some may argues we can use polynomial regression instead, but it may raise underfitting and overfitting problems.

So, we would like to use neural networks to solve this problem.

## Neural Networks

Data from axon to synapse, then through dendrite to a cell boday. After activation, the data will be sent to the next layer through axon.

We have many different types NN, such as feed-forward NN, recurrent NN, convolutional NN, etc. In this course, we will focus on feed-forward NN.

## Common used activation functions

Linear function: $y = z$

Hard Threshold function: $y = \begin{cases} 1, & z \geq 0 \\ 0, & z < 0 \end{cases}$

logistic function: $y = \frac{1}{1 + e^{-z}}$

Hyperbolic tangent function: $y = \frac{e^z - e^{-z}}{e^z + e^{-z}}$

*Rectified Linear Unit (ReLU)*: $y = \max(0,z)$  (the common used one)

Soft ReLU: $y = \log(1 + e^z)$