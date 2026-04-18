---
title: "Graph"
--- 

A **graph** $G= (V, E)$ is a pair of sets $(V, E)$ where  $V$ is a set of vertices and $E$ is a set of edges. 

-   If $E$ is a set of unordered pairs, the graph is called **undirected**. If $E$ is a set of ordered pairs, the graph is called **directed**.
    -   if self-loop allowed in undirected graph depend on given questions.
-   **Weight** of edge is a function $w : E \to \mathbf{R}$ where $w(\{u,v\})$ is the weight of edge $\{u,v\}$
-   A **matching** $M\subseteq E$ is a subset of edges that those edges that do not share any end points 
    -   every vertex in one matching then this matching is perfect 
-   two vertices $u,v$ are **adjacent** if $\{u,v\}\in E$
    -   one is called neighbor of the other
    -   an edge (*u*,*v*) is **incident on** vertices *u* and *v*. In a directed graph, the terminology differentiates between the beginning and ending vertex of an edge. So edge (*u*,*v*) which **leaves** vertex *u* is said to be **incident from** vertex *u* and is **incident to** (or **enters**) vertex *v*
-   A sequence of distinct vertices $(v_1,\ldots, v_n)$ is a **path** from $v_1$ to $v_n$ if for every $i\in \{1,\ldots, n-1\}, v_i$ and $v_{i+1}$ are adjacent. 
    -   The **length** of the path is the number of edges in the path.
    -   A **simple** path contains no repeated edge
-   A sequence of distinct vertices $(v_1,\ldots, v_n)$ is a the **cycle** if $(v_1,\ldots, v_n)$  is a path,  $v_1 = v_n$ and $\{v_{n-1}, v_n\in E\}$
    -   A cycle is called **Hamiltonian** if every vertex appear in the cycle exactly once (except for the start/end vertex which appears twice)
    -   A **simple** circle contains no repeated edge
-   A $k$**-(vertex) coloring** of $G$ is a function $f: V\to C$ , $\forall u,v \in V, \{u,v\}\in E \lor \{v,u\}\in E \implies f(u) \ne f(v)$
-   **Connected**: $\forall u,v \in V,  v\ne u$ there is some path from $u$ to $v$
-   **acyclic**: no cycle in graph
-   **independent set**: $I \subseteq V$ , $\forall v,u\in I, \nexists e\in E, e = \{v,u\}\lor e=\{u,v\} \implies I$ is an independent set 
-   In an undirected graph, the **degree** of a vertex $\nu$ is the number of edges incident on $\nu$ . In a directed graph, the **in-degree** of vertex $\nu$  is the number of edges incident to $\nu$  (the size of set $\{(x,\nu):x\in E\}$) and the **out-degree** is the number of edges incident from *v* (the size of set $\{(\nu,x):x\in E\}$).
- A **connected component** is a group of nodes that are connected by edges

The adjacvency-list representation of a graph $G = (V,E)$ consists of an array <i> Adj </i> , one for each vertex in $V$. For each $u\in V$, the adjacency list $Adj[u]$ contains all the vertices $\nu$ such that $(u,\nu)\in E$.
- Use space complexity $O(|V|+|E|)$

The adjacency-matrix representation of a graph $G = (V,E)$ consists of a matrix $Adj$ such that $Adj[u][v]$ is 1 if $(u,v)\in E$ and 0 otherwise where this such matrix is $|V|\times|V|$.
- Use space complexity $O(|V|^2)$

We always prefer the adjacency-list representation of a graph because it is more space-efficient than the adjacency-matrix representation and get more robustness in which we can augment on the node of the linked list so that we can present weight graph.

Some examples about Graph:

-   locations on maps, relationship between people(contact facing), Courses, WIFI Connection, Trees, vector graph, airport  routes, functions, binary relations

Matching Problem:

-   input: a graph with weight
-   output: A matching (usually maximum/minimum)

Pathing Finding Problem:

-   Input: a graph and two vertices
-   output: A path between two vertices

Travelling Salesman Problem:

-   Input: a graph and a start vertex
-   Output: a Hamiltonian cycle minimizes the total edge weights

Coloring Problem:

-   input: a graph
-   output a k-coloring of the graph

Independent Set Problem:

-   input: a graph, a number $k\in \N$ with $k>1$
-   output: An independent set $I \subseteq V\in G$ of size $k$