# Ordered Set

An augmented AVL Trees, where for each node we have a new attribute node named count.

`rank(k):` return k's position from bottom

`select(r):` return the object on r from bottom

e.g. for $\{27,50,15,9,34,12\}$  $rank(34) = 5, select(3) = 15$

## Implement

**Insert:** after insert node, update the count of nodes.

**Rank:** Since the order always maintain, then we can just direct count the number of node to get rank. If k exists, then we start with a residue with 0. Whenever we compare with current root we update residue:

1.   if root equal to k, then the rank equal to its left tree's count + residue + 1. 
2.   If root less than k, then residue = residue + root's left tree's count + 1, and then move forward to compare with right tree
3.   if root greater than k, then move forward to compare with left tree

**Select:** similar idea with rank, but compare with nodes' count:

1.   if 1 + root left tree's count + residue  == r, then root is what we want
2.   if 1 + root left tree's count + residue > r,  residue = residue + root's left tree's count + 1,  and then we move forward to compare with right tree
3.   if 1 + root left tree's count + residue < r, then we move forward to compare with left tree

## Worst-Case Time complexity

| Operation | Time Complexity |
|:---------:|:---------------:|
| Rank      | O(log n)        |
| Select    | O(log n)        |
