# Binomial Heap

Binomial Heap is a **mergeable heap** is a heap data structure implements by a collection of binomial trees follwing the binomial heap properties: 

1. Each binomial tree of binomial heap obeys the min-heap property which is min-heap-oredered.
2. For any nonnegative integer $k$, there is at most one binomial tree in heap whose root has degree $k$. That is, for a $n$ node binomial heap, there are at most $\lfloor \lg n \rfloor + 1$ binomial trees in the heap.

Before we go further, in case, Binomial Tree follows:

1. totally $2^k$ nodes in this tree
2. $k$ is the height of the tree
3. at each depth, there are ${k \choose i}$ nodes for $i = 0, 1, \dots, k$
4. the root of this tree has the biggest degree $k$.
5. If children of the root are numbered by $k-1, k-2, \dots, 0$, then this children $i$ is root of a sub binomial tree of degree $i$.

Furthermore, a node of binomial heap with 4 attributes: parent, child, sibling, and key.

## Implement

`Binomial-Heap-Minimum(H)`: return the node with the minimum key in the binomial heap $H$ where we go through the root list of $H$ and find the node with the minimum key.

`Binomial-Heap-Union(H1, H2)`: return a binomial heap $H$ that contains all the nodes of $H1$ and $H2$. It basically create a empty binomial heap and repeatedly links binomial trees whose whose roots have the same degree. Since two binomial trees satisfied the binomial heap properties, then we can use `Binomial-Heap-Link` to link them where make one of them as the child of the other.

`Binomial-Heap-Link(y, z)`: link `y` to `z`. Since they have the same degree, then we use the property of binomial tress to do that linking. Specifically, we make `y` the child of `z` and increase the degree of `z` by 1 and do updating for other attributes of heap node.

`Binomial-Heap-Insert(H, x)`: insert a node `x` into the binomial heap `H`. It basically create a binomial heap `H1` with only one node `x` and then use `Binomial-Heap-Union` to merge `H` and `H1`. Then we return the new binomial heap which created by `Binomial-Heap-Union`.

`Binomial-Heap-Extract-Min(H)`: extract the node with the minimum key from the binomial heap `H`. It basically find the node with the minimum key in the root list of `H` and remove it from the root list. Then we create a binomial heap `H1` with the children of the node we just removed. Then we use `Binomial-Heap-Union` to merge `H` and `H1`. Then we return the new binomial heap which created by `Binomial-Heap-Union`. (Note that we remove the subtree rooted at the node with the minimum key from the root list of `H` and then merge the children of this node with the root list of `H`.)

`Binomial-Heap-Decrease-Key(H, x, k)`: first notice that we can only decrease the key else we will raise the error. Then base on our implementation of `Binomial-Heap` we have parent, children and sibling attributes for each node. So we can use these attributes to do the decrease key operation. Specifically, we decrease the key of `x` to `k` and then we check if the heap property is violated. If it is violated, then we swap the key of `x` and its parent. Then we continue to check the heap property until it is satisfied. (Note that we also need to update all attributes of those two nodes)

`Binomial-Heap-Delete(H, x)`: delete the node `x` from the binomial heap `H`. It basically decrease the key of `x` to $-\infty$ and then extract the node with the minimum key from the binomial heap `H`. Then we return the new binomial heap which created by `Binomial-Heap-Union`.

## Worst-Case Time complexity

| Operation | Binary Heap (worst-case) | Binomial Heap (worst-case) | Fibonacci Heap (amortized) |
|:----------|:------------|:--------------|:---------------|
| MAKE-HEAP | $\Theta(1)$ | $\Theta(1)$ | $\Theta(1)$ |
| INSERT | $\Theta(\lg n)$ | $\mathcal{O}(\lg n)$ | $\Theta(1)$ |
|MINIMUM | $\Theta(1)$ | $\mathcal{O}(\lg n)$ | $\Theta(1)$ |
|EXTRACT-MIN | $\Theta(\lg n)$ | $\Theta(\lg n)$ | $\mathcal{O}(\lg n)$ |
|UNION | $\Theta(n)$ | $\mathcal{O}(\lg n)$ | $\Theta(1)$ |
|DECREASE-KEY | $\Theta(\lg n)$ | $\Theta(\lg n)$ | $\Theta(1)$ |
|DELETE | $\Theta(\lg n)$ | $\Theta(\lg n)$ | $\mathcal{O}(\lg n)$ |