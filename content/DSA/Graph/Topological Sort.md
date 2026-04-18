A **topological sort** of a directed acyclic graph $G = (V,E)$ is a linear ordering of all its vertices such that if $(u,v)\in E$, then $u$ appears before $v$ in the ordering. We can use DFS to find a topological sort of a directed acyclic graph $G = (V,E)$.
Steps with precondition DAG $G = (V,E)$:
1. Call DFS(G) to compute finishing times $v.f$ for each vertex $v$.
2. as each vertex is finished, insert it onto the front of a linked list.
3. return the linked list of vertices.

A directed graph $G$ is acyclic $\iff$ a depth-first search of $G$ never produces a back edge.

The topological sort algorithm take $O(|V|+|E|)$ time.