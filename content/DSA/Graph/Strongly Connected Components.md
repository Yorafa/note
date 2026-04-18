A directed graph $G = (V,E)$ is **strongly connected** $\iff$ for every pair of vertices $u,v\in V$, there is a path from $u$ to $v$ and a path from $v$ to $u$.

Using Edge and Transpose Edge, we can find the strongly connected components of a directed graph $G = (V,E)$.

Steps:

1. Call DFS(G) to compute finishing times $v.f$ for each vertex $v$.
2. compute $G^T$.
3. call DFS(G^T), but in the main loop of DFS, consider the vertices in order of decreasing $v.f$ (as computed in line 1).
4. output the vertices of each tree in the depth-first forest formed in line 3 as a separate strongly connected component.

**Component Graph**: Suppose $G$ has $C_1, \ldots, C_k$ strongly connected components. Then we define $V^{SCC} = \{v_1,\ldots,v_k\}$ and $\forall v\in V^{SCC}$, $v_i$ is the representative of $C_i$. We define $E^{SCC} = \{(v_i,v_j)|\exists u\in C_i, v\in C_j, (u,v)\in E\}$. Then $G^{SCC} = (V^{SCC}, E^{SCC})$ is a directed acyclic graph.

Let $C$ and $C'$ be distinct strongly connected components in directed graph $G$. Let $u,v\in C$ and $u',v'\in C'$, and suppose $G$ contains a path from $u$ to $u'$, then $G$ cannot also contain a path from $v‘$ to $v$.

Let $C$ and $C'$ be distinct strongly connected components in directed graph $G$. Suppose edge $(u,v)\in E$ where $u\in C$, $v\in C'$. Then $f(C) \ge f(C')$.
