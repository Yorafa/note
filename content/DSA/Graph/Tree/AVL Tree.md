# AVL Tree

A tree is an **AVL Tree** if it is [binary search tree](Binary%20Search%20Tree.md) and AVL balanced.

-   We first define the balance factor \= \#height of right subtree -  \#height of left subtree
-   **AVL balanced** means that each node of this tree satisfied balance factor in range $[-1, 1]$
-   we also call balance factor in range $[-1, 1]$ as **AVL invariant**

AVL have the same methods as the BST do, but need more about keep balanced

## Implement

To have AVL Tree, we should modify the implement of BST.

**Insert:** The same insert with modify the height of node to track if balance factor. After insert, check the AVL invariant if satisfied. If not, then we need to do rebalance/rotation.

**Delete**: The same delete with modify the height of node to track if balance factor. After delete, check the AVL invariant if satisfied. If not, then we need to do rebalance/rotation.

**Rebalance:** base on balance factor negative or not, we will swap left/right children with parent; more specifically, we have 4 cases  after insert/delete:

1.    insert/delete right, then left tree's right's height > left tree's left's: rotate left about left tree and then rotate right about root
2.    left tree's right's height \<\= left tree's left's: rotate right about root
3.    insert/delete left,  then right tree's left's height > right tree's right's: rotate right about right tree and then rotate left about root
4.    right tree's left's height \<\= tree's right's: rotate left about root

**Rotation:**

1.   rotate left: swap root with right tree where root new right \= right tree's left and right tree's left \= root;
2.   rotate right: swap root with left tree where root new left \= right tree's right and left tree's right \= root;

Code in python given in lec:

```python
def AVL-INSERT(root, x):
    if root is NIL:  # found insertion point
        root = TreeNode(x)  # initial height = 0
    elif x.key < root.item.key:
        root.left = AVL-INSERT(root.left, x)
        root = AVL-REBALANCE-RIGHT(root)
    elif x.key > root.item.key:
        root.right = AVL-INSERT(root.right, x)
        root = AVL-REBALANCE-LEFT(root)
    else:  # x.key == root.item.key
        # Just replace root's item with x -- nothing else changes.
        root.item = x
        return root

def AVL-REBALANCE-LEFT(root):  # Precondition: root is not NIL
    # Recalculate height.
    root.height = 1 + max(root.left.height, root.right.height)
    # Rebalance if necessary.
    if root.right.height > 1 + root.left.height:
        # Perform double rotation if necessary.
        if root.right.left.height > root.right.right.height:
            root.right = AVL-ROTATE-RIGHT(root.right)
            root = AVL-ROTATE-LEFT(root)
            return root

def AVL-REBALANCE-RIGHT(root):  # Precondition: root is not NIL
    # Recalculate height
    root.height = 1 + max(root.left.height, root.right.height)
    # Rebalance if necessary.
    if root.left.height > 1 + root.right.height:
        # Perform double rotation if necessary.
        if root.left.right.height > root.left.left.height:
            root.left = AVL-ROTATE-LEFT(root.left)
            root = AVL-ROTATE-RIGHT(root)
            return root
        
def AVL-ROTATE-LEFT(parent): # Precond: parent != NIL, parent.right != NIL
    # Rearrange references.
    child = parent.right
    parent.right = child.left
    child.left = parent
    # Update heights.
    parent.height = 1 + max(parent.left.height, parent.right.height)
    child.height = 1 + max(child.left.height, child.right.height)
    # Return new parent.
    return child

def AVL-ROTATE-RIGHT(parent): # Precond: parent != NIL, parent.left != NIL
    # Rearrange references.
    child = parent.left
    parent.left = child.right
    child.right = parent
    # Update heights.
    parent.height = 1 + max(parent.left.height, parent.right.height)
    child.height = 1 + max(child.left.height, child.right.height)
    # Return new parent.
    return child

def AVL-DELETE(root, x):
    if root is NIL:
        pass  # nothing to remove
    elif x.key < root.item.key:
        root.left = AVL-DELETE(root.left, x)
        root = AVL-REBALANCE-LEFT(root)  # careful with direction!
    elif x.key > root.item.key:
        root.right = AVL-DELETE(root.right, x)
        root = AVL-REBALANCE-RIGHT(root)  # careful with direction!
    else:  # x.key == root.item.key
        if root.left is NIL:
            root = root.right  # includes case root.right is NIL
        elif root.right is NIL:
            root = root.left
        else:
            # Select whether to replace root.item with its predecessor or
            # its successor, depending on the heights of subtrees.
            if root.left.height > root.right.height:
                root.item, root.left = AVL-DELETE-MAX(root.left)
            else:
                root.item, root.right = AVL-DELETE-MIN(root.right)
                # Height might have changed, but no rebalancing for root.
                root.height = 1 + max(root.left.height, root.right.height)
                return root

def AVL-DELETE-MIN(root):
    if root.left is NIL:
        return root.item, root.right
    else:
        item, root.left = AVL-DELETE-MIN(root.left)
        root = AVL-REBALANCE-LEFT(root)
        return item, root

def AVL-DELETE-MAX(root):
    if root.right is NIL:
        return root.item, root.left
    else:
        item, root.right = AVL-DELETE-MAX(root.right)
        root = AVL-REBALANCE-RIGHT(root)
        return item, root


def AVL-SEARCH(root, k):
    if root is NIL:  # k not in root's subtree
        pass  # NIL will be returned below
    elif k < root.item.key:
        root = AVL-SEARCH(root.left, k)
    elif k > root.item.key:
        root = AVL-SEARCH(root.right, k)
    else:  # x.key == root.item.key
        pass  # root is the node we want
    return root
```

## Worst-Case Time Complexity

| Operation | Time Complexity |
|:---------:|:---------------:|
|   Search  |      O(log n)   |
|   Insert  |      O(log n)   |
|   Delete  |      O(log n)   |


