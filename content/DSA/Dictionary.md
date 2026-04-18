# Dictionary

Dictionary is famous ADT in python (.net). In other programming language we call it map or something else. They are almost the same things, but called different in the different language. For each item in the collection dictionary, the item.key should be unique, that is, why we call it dictionary where a stuff usually have a unique name. For dictionary, we should have:

`Insert(S, x):` Insert item x into dictionary S. If key of x already existed, modify its value to x's value.

`Search(S, k):` Return x in S with x.key = k or null no such x exists.

`Delete(S, x):` Delete whole x from S

## Implement

Usually implemented by Red-Black-Tree and hashing for the best time complexity. The easy way could be a simple BST with given priority, that is, insert, search and delete with best  $O(\log n)$ time complexity and $O(n)$ with the worst case (RBT make all $O(\log n)$). To enhance it, we also can use AVL Tree which easier than RBT, but also make all $O(\log n)$
