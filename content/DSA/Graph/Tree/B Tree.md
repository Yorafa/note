Multi-children self-balanced ordered tree. A B tree with order `m` should satisfied:

1. all leaves in the same level
2. balanced and ordered
3. at most `m` children and `m - 1` element in the node. at least `2` children and `1` element for leave, `ceil(m/2)` children and `ceil(m/2) - 1`elements for others, except root.
