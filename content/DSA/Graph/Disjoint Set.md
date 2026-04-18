# Disjoint Set

Sometime you may call Disjoint Set as Union-Find Set.

A disjoint-set data structurtre maintains a collection $S = \{S_1, S_2, \dots, S_n\}$ of disjoint dynamic sets. We identify each set by a representative member.

We can perform the following operations on a disjoint-set data structure:
1. **MakeSet(x)**: Create a new set containing only $x$.
2. **Union(x, y)**: Combine the dynamic sets containing $x$ and $y$ into a new set that is the union of these two sets.
3. **Find(x)**: Return the representative member of the set containing $x$.

using the linked-list representation of a disjoint-set data structure, we have amortized time complexity of $O(m + n\log n)$ for $m$ operations and $n$ make-set operations.


using the union-by-rank and path compression heuristics, we have amortized time complexity of $O(m\alpha(n))$ for $m$ operations and $n$ make-set operations, where $\alpha(n)$ is the inverse Ackermann function, and $\alpha(n) \approx \lg^*n$ like $O(5m)$