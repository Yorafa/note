# Recurrence

A recurrence is in **standard form** if it is written as $T(n) = aT(n/b) + f(n)$. For some constants $a\ge 1, b > 1$, and some function $f: \N \to \R$

- $a:$ the branching factor of the tree (how many children)
- $b:$ the reduction factor (length compare to main)
- $f(n)$: the time complexity of non-recursive work
- The height of the tree is $log_b(n)$
- The number of vertices at level $h$ is $a^h$
- The total non-recursive work done at level $h$ is $a^hf(n/b^h)$
  - Root Work. $f(n)$
  - Leaf Work. $a^{log_b(n)} f(1) = \Theta(n^{log_b(a)})^1$
- Summing up the levels, the total amount of work done is $\sum_{h= 0} ^{log_b(n)} a^hf(n/b)$

### Master Theorem

We always use **Master Theorem** to solve such standard form; Let $T(n) = aT(n/b) + f(n)$, then there are three cases defined by the leaf work:

1.  Leaf heavy: $f(n) = O(n^{log_b(a) - \epsilon})$ for some constant $\epsilon > 0$

2.  Balanced: $f(n) = \Theta(n^{log_b(a)})$

3.  Root heavy: $f(n) = \Omega(n^{log_b(a) + \epsilon})$ for some constant $\epsilon > 0$, and $af(n/b) \le cf(n)$ for some constant $c < 1$ for all sufficiently large $n$ (Regularity Condition)

Combine those cases, we have: $T(n) = \begin{cases} \Theta(n^{log_b(a)})  & \text{Leaf heavy Case} \\ \Theta(n^{log_b(a)}log(n))  & \text{Balanced Case}  \\\Theta({f(n)})  & \text{Root heavy Case}  \end{cases}$

Base on this, we:

1.  Write the recurrence in normal form to find the parameters $a,b,f$
2.  Compare $n^{log_b(a)}$ to $f$ to determine the case split
3.  Read off the asymptotics from the relevant case

Simplified Master Theorem: let $f = n^c$ $T(n) = \begin{cases}\Theta(n^{\log_b(a)}) & a> b^c \\ \Theta(n^c \log(n) & a = b^c) \\ \Theta(n^c) & a <b^c \end{cases}$

### Generally

For a recurrences, we can simply use $r^n$ to judge the time complexity. For example, the Fibonacci:

- Assume the time complexity of $P(k+1)$ is $r^{k+1}$, and $P(k+1) = P(k) + P(k-1)$ has time complexity of $r^k$ and $r^{k-1}$
- then we have $r^{k+1} \ge r^k + r^{k-1}\implies r^{k+1} - r^k - r^{k-1}\ge 0 \implies r^{2} - r - 1 \ge 0$

To prove $T = \Theta(f)$:

First prove $T = O(f)$

1.  Remove all the floors and ceilings from the recurrence $T$
2.  Make a guess for $f$ such that $T(n) = O(f(n))$
3.  write out the recurrence: $T(n) = \ldots$
4.  whenever $T(k)$ appears on the RHS of the recurrence, substitute it with $cf(k)$
5.  Try to prove $T(n) \le cf(n)$
6.  Pick $c$ to make your analysis work

Then use the same way to prove $\Omega(f)$

# Correctness

When we have a function, how can we show the function we write is correct?

Formally, we define the input and output, and try to prove input $\implies $ output

That is, after we have the definition of input and out, then we do following to prove a function's correctness:

1.  define loop invariant
2.  Initialization
3.  Maintenance(inductive step)
4.  Termination
5.  Descending sequence

Actually, this part is the most tough part of the course where sometimes hard to find a intuitive way to prove correctness.
