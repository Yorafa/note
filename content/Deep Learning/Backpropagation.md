# Backpropagation

We define backpropagation as the reverse mode automatic differentiation. Or basically, it is the chain rule applied to neural networks.

We would like to use computation graph to illustrate the backpropagation. A **computation graph** is a directed graph where each node correspond to perations or variables.

- variables can feed their values into opeartions.
- operations can feed their output into other operations.
- every node defines a function of the variables.

In this course, when we use $\bar x$ for some variable $x$, we mean the derivative of the output with respect to $x$, i.e. $\bar x= \frac{\partial y}{\partial x}$. We also call it as **error signal**.

The full backpropagation algorithm is as follows:

1. Let $v_1,\ldots,v_n$ be a **topological ordering** (recall the topological sort) of the computation graph. $v_n$ denotes the variable we are trying to compute derivatives of.
2. First, do forward pass to compute the value of each variable.
   1. for $i = 1, 2, \ldots, n$: Compute $v_i$ as a function of $\pi(v_i)$, the parents of $v_i$.
3. then do backword pass, set $\bar v_n = 1$ (the derivative of the output with respect to itself is 1)
   1. for $i = n-1, n-2, \ldots, 1$: $\bar v_i = \sum_{j\in \text{children}(v_i)} (\frac{\partial v_j}{\partial v_i})^T\bar v_j$

The computational cost:

- Forward pass: one add-multiply operation per weight
- Backward pass: two add-multiply operation per weight (about 2x as much as forward pass)
- for a multilayer perceptron, the computational cost is is linear in the number of layers and quadratic in the number of units per layer.

## Confusing Terminology

Automatic differentiation (autodiff): a general technique for computing a value and constructing a procedure for computing its derivative.

Backpropagation: a specific algorithm for computing derivatives of *neural networks*.

Autograd: a Python library for automatic differentiation.

## More deeper into backpropagation

Since backprop is a autodiff algorithm, we want to know more about autodiff to understand backprop better.

An autodiff system will convert the program into a sequence of *primitive operations* (ops) which have specified routines for computing derivatives. For example, we have two functions $y = ax + b$ and $z = y^2$. We can convert them as $t_1 = ax, y = t_1 + b, z = y^2$. That is, we can do the derivative of each operation easily. i.e. autograd tracing this route through forward pass.

For each primitive operation, we must specify VJPs for each its arguments (i.e. `defvjp`) such function always with format which takes inthe output gradient, the answer (i.e. the output of the function), and the inputs to the function, and returns the input gradients. example:

```python
# y = kx + b
defvjp(multiply, lambda g, ans, x, k: g * k)
defvjp(add, lambda g, ans, x, b: g)
# z = y^2
defvjp(square, lambda g, ans, y: g * 2 * y)
```

Specifically, the VJP in the backprop represent the messages. Recall the computation graph, each node reeives a bunch of messagess from its children and aggregates them into a single

### Question

1. why we still need to def vjp in the code? why not just use the vjp function in the autograd library?
