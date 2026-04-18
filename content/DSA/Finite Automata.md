Basic definition:

- An **alphabet** $\Sigma$ is a non-empty, finite, set of symbols.
- A **string** _w_ over an alphabet $\Sigma$ is a finite (0 or more) sequence of symbols from $\Sigma$, an empty string denote by $\epsilon$
- The set of all strings is denoted $\Sigma^*$
- A **language** is any subset of $\Sigma^*$

---

**Deterministic finite automaton** (DFA): input $w \in \Sigma^*$ $\implies $ output

- Same state and same read character $\implies$ same next state (Deterministic)
- Finite number of states (finite)
- no empty string && each character only appear once && arrow for each charter in $\Sigma$

Steps:

1.  Predefined start state
2.  reads input (per char at a time). Depend on the character read and current state, deterministically moves to a new state
3.  Finish reading, check if accept states. If accept, then accept. Otherwise rejects. (double circle accept)

Let $M$ be a DFA, the language of a DFA denoted $L(M)$ is the set of strings $w\in \Sigma^*$ such that $M$ accepts $w$.

The template of defining a DFA:

1.  Fix the alphabet, $\Sigma$ of the DFA
2.  Define a finite set of states $Q$
3.  A start state $q_{start} \in Q$
4.  Define a subset $F\subseteq Q$ are accept states
5.  $\forall q\in Q$ , $\forall x\in \Sigma,$ define $y\in Q$ , $x\land q\implies y$

---

Nondeterministic finite automaton(NFA):

- Allow empty string $\epsilon$, character can appear more times or 0 times

- Same state and same read character $\implies$ same next state (Deterministic)

- Finite number of states (finite)

Steps:

1.  Predefined start state
2.  reads input (per char at a time). Depend on the character read and current state, deterministically moves to a new state
    1.  no such input appear in some arrow, immediately reject
3.  Since same character can appear many times, we need to make choice. That's, NFA accepts the string if any sequence of choices leads to an accept state

Let $N$ be a NFA, the language of a NFA denoted $L(N)$ is the set of strings $w\in \Sigma^*$ such that $N$ accepts $w$.

---

Let $A, B$ be any language over $\Sigma^*$.

- There is a DFA $M$ such that $A = L(M) \iff \exists N$ is a NFA such that $A = L(N) \iff A$ is regular
- $A$ is regular if there is a DFA $M$ such that $L(M) = A$.
- The complement of $A$ denote $\overline A =\Sigma^*\backslash A$
- The concatenation of $A$ and $B$ denote $AB = \{ab:a\in A, b\in B\}$ is the set of strings that your get by concatenating a string in $A$ and a string in $B$
- $\forall n \ge 1$, define $A^n = \{a_1a_2\cdots a_n:a_i\in A, \forall i, 1\le i \le n\}$. Let $A^0 = \{\epsilon\}$.
- $A^* = \bigcup_{i \in \N} A^i$, called Kleene star, or "A star"

---

Let $A, B$ be any language over $\Sigma$. $\forall x,y,w\in \Sigma^*$, $xw\in A \text{ XOR } yw\in A\implies w$ is **distinguisher** for $x, y$

Define a binary equivalence relationship $\sim$ relative to language A over $\Sigma^*$ as $\sim_A$, $\forall x,y\in \Sigma^*, x\sim_A y\iff \lnot \exists $ a distinguisher for $x,y \iff \forall w\in \Sigma^*. (xw\in A \iff yw \in A)$. In this situation, we say $x$ is indistinguishable from $y$ relative to $A$.

**Myhjill-Nerode Theorem**: Let $A$ be language over $\Sigma^*$. $A$ is regular $\iff \sim_A$ has a finite number of equivalence classes.

- To prove not regular, we can find an infinite set $S$ s.t. any two elements $x,y \in S$ are distinguishable. In other words, Let $A$ be a language. A set $S$ is infinite $\land \forall x,y\in S, x\ne y\land x\nsim_A y \implies A$ is not regular

Define $\delta: Q\times \Sigma^*\to Q$. $\forall x,y\in \Sigma^*, \delta(q_0,x) = \delta(q_0,y) \implies x\sim_A y$
