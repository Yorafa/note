# Induction

Almost every courses teach induction

**Basic Induction**: To prove $\forall n\in \N, (P(n))$ use some base case and induction to prove for all.

-   $(P(0) \land \forall k \in \N. (P(k)\implies P(k+1))) \implies \forall n\in \N, (P(n))$
-   we have some flexibility on basic case where if we have goal to prove $\forall n\ge1$ then we will prove $P(1)$

Basic Induction prove template:

```
Prove by induction.
Base case: [Prove P(0) is true]
Inductive step: Let k be arbitrary natural number, and assume P(k). we will show P(k+1)
```

**Complete Induction**: To prove $\forall n\in \N, (P(n))$ use some base case and more induction steps to prove for all.

-   $(P(0) \land \forall k \in \N. (P(0)\land P(1) \land \ldots\land P(k)\implies P(k+1))) \implies \forall n\in \N, (P(n))$
-   similarly, we have flexibility on basic case.

Complete Induction prove template:

```
Prove by induction.
Base case: [Prove P(0) is true]
Inductive step: Let k be arbitrary natural number, and assume for every natural number i less equal than k, P(i) . we will show P(k+1)
```

A set **generated** from $B$ (basic set) by the functions in $F$ (a set of functions $: U^m\to U$ where $U$ stand for universe set of $B$) is the set of elements that can be obtained by applying $f\in F$ to $b\in B$ a finite number of times.

**Structural Induction**: Let $C$ be a set generated from $B$ by $f\in F$. $(\forall b\in B, P(b)) \land (\forall f\in F$ on $m$ inputs $\forall a_1,\ldots,a_m \in C, (P(a_1)\land P(a_2)\land \ldots \land P(a_m)) \implies P(f(a_1,\ldots,a_m))) \implies \forall x\in C. (P(x))$

Define a **construction sequence** $S$ of length $n$ as $(x_0,\ldots,x_n)$ where $\forall x_i\in S, x_i\in B \lor x_i=f(x_{j_1},\ldots, x_{j_m}), f\in F, j_1,\ldots,j_m < i$.

The **length** of a construction sequence is represented by some measure of complexity of the object.

## WOP 

WOP(Well Ordering Principle): $\forall S\subseteq \N(S\ne \emptyset), S$ has a **minimal element**.

-   let $a\in S, \forall b\in S, a\le b \implies a$ is a minimal element 

We can use WOP to prove induction statements of the form $\forall n\in \N, (P(n))$:

1.   Check $P(b)$ is true, $b$ stand the basic case
2.   By contradiction, assume $\exists n\in \N.(\lnot P(n))$. So the set $S = \{n\in\N: \lnot P(n)\}$ is non-empty
3.   By the WOP, $S$ has a minimal element, denote as $m$; commonly, $m$ is the smallest natural number for which $P$ doesn't hold.
4.   Derive the contradiction by showing $P(m)$ or by finding a $m' < m$, for which $\lnot P(m')$
