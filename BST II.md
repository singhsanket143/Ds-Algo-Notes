
### BST AND BT MIXED
**Q1- Longest Consecutive Subsequence in a Binary Tree*

**Q2- Cousins in Binary Tree**

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

**Q4- Given the preorder traversal of the BST, find the leaf nodes of the BST.**

**Q5- Given a BT, and distance between two nodes, tell the distance between the two nodes.**

**Q6- Given the preorder traversal of a BST, construct the BST out of it.**

**Q7- Target Sum pair in BST**

===============
### Balanced Binary Search Tree

**Q1- Given a BST, convert it into a BBST**

**Q2- Given a BST, make a BST iterator**
