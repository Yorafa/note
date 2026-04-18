# Optimization

How do we train models using gradient? And how do we solve the issues of gradient (i.e. learning rate). One way is to do derivative again. That is, We have **Hessian Matrix** which is a symmetric matrix.

Locally, a function can be approximated by its second-order Taylor approximation around a point $\theta_0$: $\mathcal{J}(\theta) \approx \mathcal{J}(\theta_0) + \nabla_{\theta} \mathcal{J}(\theta_0)^T(\theta - \theta_0)  + \frac{1}{2}(\theta - \theta_0)^T H(\theta_0)(\theta - \theta_0)$.

- $H$ also represent the curvature of the function. for some vector $v$, $v^T H v > 0$ leads the cost function curves upwards (i.e. positive curvature, positive definite). When $v^T H v < 0$, the cost function curves downwards (i.e. negative curvature).
  - $v^T H v \ge 0$  then the cost function is smooth and convex which means has no spurious local minima.
- We can also have the spectral decomposition of the Hessian matrix: $H(\theta_0) = Q \Lambda Q^T$, where $Q$ is an orthogonal matrix and $\Lambda$ is a diagonal matrix. (i.e. the eigenvector matrix and eigenvalue matrix)

The problems are that the permutation symmetries (H property) will lead non-convex when we train nn with hide units.

## Problems and Solutions

$H$ with some large positive eigenvalues and some eigenvalues close to zero, such situation be known as **ill-conditioned curvature** (e.g. GD may be slow to converge). That is, we bounded learning rate by ill-conditioned curvature where $\alpha < 2/\lambda_{max}$ to avoid divergence. And also $\lambda_{max}/\lambda_{min}$ known as **condition number** where larger condition number leads to slower convergence.

To avoid the problem lead by ill-conditioned curvature, we usually normalized the input data to have zero mean and unit variance especially when they're in arbitrary units by $\tilde{x}_{j} = \frac{x_{j} - \mu_{j}}{\sigma_{j}}$.

For hidden units may have non-centered activation functions, we usually use:

- replace logistic units with tanh units, or
- use batch normalization which explicitly centers the activation function.
- momentum

### Momentum

**Momentum** is a simple and highly effective method to deal with ill-conditioned curvature. Formally, we have: $p \leftarrow \mu p - \alpha \frac{\partial \mathcal{J}}{\partial \theta}$ and then $\theta \leftarrow \theta + p$.

- $\mu$ is the damping parameter which is usually set to 0.9/0.99. (slightly less than 1)

If we have a constant gradient, then the termianl velocity is $- \frac{\alpha}{1 - \mu} \frac{\partial \mathcal{J}}{\partial \theta}$.

## Ravines

Although most ill-conditioned curvature problems can be solved by momentum, normalization, there are still some problems that cannot be solved by momentum. For example, the **ravines** problem.

The second-order optimization by use curvature information is a good idea to solve it but too complicated and difficult to scale to large nn and large datasets.

One way is call Adam, beyond that let's introduce RMSprop.

### RMSprop

**RMSprop** is a variant of GD which rescales each coordinate of the gradient to have norm 1 on average (i.e. normalize the gradient) by: $s_j \leftarrow (1 - \gamma)s_j + \gamma [\frac{\partial \mathcal{J}}{\partial \theta_j}]^2$ and then $\theta_j \leftarrow \theta_j - \alpha \frac{1}{\sqrt{s_j + \epsilon}} \frac{\partial \mathcal{J}}{\partial \theta_j}$.

We can always use it once it satisfies axis-aligned.

Adam = RMSprop + Momentum

more about [Adam](https://arxiv.org/pdf/1412.6980.pdf) by Diedre Kingma and Jimmy Ba (our instructor).

## Special points

### Critical Points

The **critical point** is $\mathcal{J}(\theta) \approx \mathcal{J}(\theta_0) + \frac{1}{2}(\theta - \theta_0)^T H(\theta_0)(\theta - \theta_0)$. 

- for any critical point $\theta^*$, $H(\theta^*)$ exists and is positive definite $\implies \theta^*$ is a local minimum.

### Saddle Points

A **saddle point** is a point where:

- $\nabla \mathcal{J}(\theta) = 0$
- $H(\theta)$ has both positive and negative eigenvalues.
- leads stuck in local minima.

### Plateaux

A flat region is called **plateaux**. The gradient is zero, but the Hessian is positive definite.

- When such flat region appears on the activation function, it may lead the weights to be stuck in the same value. (saturated unit)
- E.g. ReLU with input always negative, the weights will be stuck in zero. (dead unit)