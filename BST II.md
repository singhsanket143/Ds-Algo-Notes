**Q1- Cousins in Binary Tree**

In a binary tree, the root node is at depth 0, and children of each depth k node are at depth k+1.

Two nodes of a binary tree are cousins if they have the same depth, but have different parents.

We are given the root of a binary tree with unique values, and the values x and y of two different nodes in the tree.

Return true if and only if the nodes corresponding to the values x and y are cousins.

```cpp
class Custom {
public:
    int depth;
    TreeNode* parent;
    Custom(int depth, TreeNode *parent) {
        this->depth = depth;
        this->parent = parent;
    }
};
class Solution {
public:
    
    Custom *helper(TreeNode* root, int x, int d, TreeNode* parent) {
        if(root == NULL) {
            return NULL;
        }
        if(root->val == x) {
            return new Custom(d, parent);
        }
        Custom *left = helper(root->left, x, d+1, root);
        if(left != NULL) {
            return left;
        }
        Custom *right = helper(root->right, x, d+1, root);
        if(right != NULL) {
            return right;
        }
        return NULL;
    }
    
    bool isCousins(TreeNode* root, int x, int y) {
        if(root == NULL) return false;
        Custom* X = helper(root, x, 0, NULL);
        Custom* Y = helper(root, y, 0, NULL);
        
        if(X->depth == Y->depth and X->parent != Y->parent) return true;
        else return false;
    }
};
```

**Q3- Given a BST, find the kth smallest element in the BST**
Approach 1: Write inorder traversal which will be in sorted form. Then find the kth smallest element.
Approach 2: 
