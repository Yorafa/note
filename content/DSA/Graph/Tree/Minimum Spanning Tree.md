# Minimum Spanning Tree

We define a **saft edge** for a subset $A$ of some minimum spanning tree if adding it to $A$ still is a part of a minimum spanning tree.

1. We define a **cut** (S, V - S) of an undirected graph $G$ is a partition of $V$.
2. We say a edge $(u,v)\in E$ **crosses** a cut (S, V - S) if $u\in S$ and $v\in V-S$.
3. We say that a cut **respects** a set $A$ of edges if no edge in $A$ crosses the cut.
4. An edge $(u,v)\in E$ is **light edge** crossing a cut (S, V - S) if its weight is the minimum weight of all edges crossing the cut.

Let $G = (V,E)$ be a connected undirected graph with a real-valued weight function $w$ defined on $E$. Let $A4 be a subset of $E$ that is included in some minimum spanning tree for $G$, let $(S, V-S)$ be any cut of $G$ that respect $A$, and let $(u,v)$ be a light edge crossing $(S, V-S)$. Then $(u,v)$ is a safe edge for $A$.


Let $G = (V, E)$ be a connected, undirected graph with a real-valued weight function $w$ defined on $E$. Let $A$ be a subset of $E$ that is included in some minimum spanning tree for $G$, and let $C = (V_C, V - V_C)$  be a connected component (tree) in the
forest $G_A = (V, A)$. If $(u,v)$ is a light edge connecting $C$ to some other component in $G_A$, then $(u,v)$ is safe for $A$.

## Kruskal's Algorithm

Kruskal’s algorithm finds a safe edge to add to the growing forest by finding, of all the edges that connect any two trees in the forest, an edge $(u,v)$ of least weight. One implementation of Kruskal’s algorithm is to use a disjoint-set data structure to keep track if two vertices are in the same tree. 

The basic idea:
1. Make a set for each vertex.
2. sort the edges in nondecreasing order of weight.
3. Union sorted edges if they are not in the same set.
4. return the set of edges that are in the same set.

The running time of Kruskal’s algorithm is $O(|E| \log |V|)$.

## Prim's Algorithm

Prim’s algorithm finds a safe edge to add to the growing forest by finding, of all the edges that connect any vertex in the forest to any vertex not in the forest, an edge $(u,v)$ of least weight. One implementation of Prim’s algorithm is to use a priority queue to keep track of the light edges that connect the forest to the rest of the graph.

The basic idea:
1. set up all keys and parents.
2. set up a min-prority heap by vertex.
3. set root key to 0 and then do while loop
4. modify the adj vertices' keys and parents by the light edges.

The running time of Prim’s algorithm is $O(|E| + |V| \log |V|)$.