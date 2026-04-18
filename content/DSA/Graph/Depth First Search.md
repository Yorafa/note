The predecessor subgraph of a DFS forms a **depth-first forest** comprising several depth-first trees. We also do timestamps for each vertex which notice the arrival time and finished time. (`u.d` denote discovered time which start from parent time + 1, `u.f` denote finished time which end with the last child time + 1). According the time structure we have properties, for a node $u, v$:

- if $[u.d, u.f]$ and $[v.d, v.f]$ are disjoint, then $u$ and $v$ are not a descendant of each other in the depth-first forest.
- if $[u.d, u.f]$ is a subset of $[v.d, v.f]$, then $u$ is a descendant of $v$ in the depth-first forest.

We also define several edges of depth-first forest:

- **tree edge**: an edge $(u,v)\in E$ such that $v.\pi = u$.
- **back edge**: an edge $(u,v) \in E$, such that $v.d < u.d$ and $v.f > u.f$. Self-loop is also a back edge.
- **forward edge**: an edge $(u,v) \in E$ such that $v.d > u.d$ and $v.f < u.f$.
- **cross edge**: all other edges.

An undirected graph $G$, every edge of $G$ is either a tree edge or a back edge.

The DFS algorithm take $O(|V|+|E|)$ time.
