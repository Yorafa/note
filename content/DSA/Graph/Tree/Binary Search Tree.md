# Binary Search Tree

Let $x$ be a node in a **Binary Search Tree(BST)**. If $y$ is a node in the left subtree of $x$, then $y.val <  x.val$. If $y$ is a node in the right subtree of $x$, then $y.val >  x.val$. That means we have a sorted list if we in-order travels (here the < and > stand for the priority).

-   The minimum of a BST is the left most node, the maximum is the right most node.
-   A **successor** of a BST is the minimum of its right children tree, or we can say as the left most node of right children tree.
-   A **predecessor** of a BST is the maximum of its left children tree.
-   When we say left/right most, means the most we can recursive the left/right 'till not.

A BST usually with the methods:

`Insert(BST, x):` Insert x into BST

`Delete(BST, x):` Delete x from BST

`Search(BST, x):` Return x if exist, or null if not exists.

## Implement

**Search:** Compare with current root, if $x.key > root.key$ then go right tree and repeat the comparison, if $<$ then go left tree and then repeat the comparison 'till equal or none.

**Insert**: Similar idea with search, but the thing is that we need a notation of current comparison's parent while comparing so that we connect the notation and this node when compare done. 

**Delete:** we do search of a node $z$, when we find it, it will be deleted with 3 cases:

1.   (no children): replace this location with NULL
2.   (1 children): replace this location with $z$'s children
3.   (2 children): replace this location's value with $z$'s successor, and replace successor's location with NULL

A c++ code below in case (different with lec/clrs):

```c++
// object already be set up, and we assume the <, > respect to the priority of object for convinence
struct BST{
    Obj obj;
    BST* left;
    BST* right:
    BST(Obj obj, BST* left=nullptr, BST* right=nullptr){
        this.obj = obj;
        this.left = left;
        this.right = right;
    }
};

bool search(BST* root, Obj x){
    if (root == nullptr) return false;
    if (x.key > root->obj.key) search(root->right, x);
    if (x.key < root->obj.key) search(root->left, x);
    return true
}

BST* insert(BST* root, Obj x){
    if (root == nullptr) return new BST(x);
    if (x.key > root->obj.key) return insert(root->right, x);
    if (x.key < root->obj.key) return insert(root->left, x);
    root->obj = x;
    return root;
}

BST* delete(BST* root, Obj x){
    if (root == nullptr) return;
    if (x.key > root->obj.key) delete(root->right, x);
    else if (x.key < root->obj.key) delete(root->left, x);
	else{
        if (root->left == nullptr) root = root->right;
        else if (root->right == nullptr) root = root->left;
        else {
            pair<Obj, BST*> remain = delete_min(root->right);
            root->obj = remain.first;
            root->right = remain.second;
        }
    }
    return root;
}

pair<Obj, BST*> delete_min(BST* root){
	if (root->left == nullptr) return {root->obj, root->right};
    pair<Obj, BST*> remain = delete_min(root->left);
    root->left = remain.second;
    return {remain.first, root};
}
```

## Worst-Case Time Complexity

| Operation | Time Complexity |
|:---------:|:---------------:|
|   Search  |   O(n)      |
|   Insert  |   O(n)      |
|   Delete  |   O(n)      |

