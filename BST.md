**Binary Search Tree**

- Extension of Binary Tree
- All nodes in left subtree will be smaller than root.
- All nodes in right subtree will be greater than root.
- Inorder traversal yields sorted ordering of the element

**How to handle equal elements?**

- Keep a count on every node by modifying the class of the node. 
- Same elements can either go in left or right subtree.

- Questions Similar to BT:
	- Size
	- Height
	- Views - left, right, top
	- Balanced
	- Diameter
	- Traversal
	
- Questions Changed 
	- Finding an element in BST
	- Max
	
- Every BST is a BT? Yes
- Every BT is a BST? No 
	
**Add a node in BST**

_Algorithm_

1. Start from root.
2. Compare the inserting element with root, if less than root, then recurse for left, else recurse for right.
3. After reaching end, just insert that node at left(if less than current) else right.

```java
public void add(int item) {

		add(this.root, null, false, item);
	}

	private void add(Node node, Node parent, boolean ilc, int item) {
		// base case
		if (node == null) { 
			Node nn = new Node();
			nn.data = item;
			if (ilc)
				parent.left = nn;
			else
				parent.right = nn;
			return;
		}
		if (item < node.data) {
			add(node.left, node, true, item);
		}
		if (item > node.data) {
			add(node.right, node, false, item);
		}
	}
```

**Delete a node in BST**

Three possibilities:
- _Node to be deleted is leaf:_ Simply remove from the tree.
- _Node to be deleted has only one child:_ Copy the child to the node and delete the child
- _Node to be deleted has two children:_ Find inorder successor of the node. Copy contents of the inorder successor to the node and delete the inorder successor. Note that inorder predecessor can also be used.

```java
public void remove(int item) {

		remove(this.root, null, false, item);
	}

	private void remove(Node node, Node parent, boolean ilc, int item) {

		if (node == null) {
			return;
		}
		if (item < node.data) {

			remove(node.left, node, true, item);
		} else if (item > node.data) {

			remove(node.right, node, false, item);
		} else {
			// Possibility 1
			if (node.left == null && node.right == null) {
				if (ilc)
					parent.left = null;
				else
					parent.right = null;
				
			} else if (node.left != null && node.right == null) {
				if (ilc)
					parent.left = node.left;
				else
					parent.right = node.left;
				this.size--;
			} else if (node.right != null && node.left == null) {
				if (ilc)
					parent.left = node.right;
				else
					parent.right = node.right;
				this.size--;
			} else {

				int max = max(node.left);
				node.data = max;

				remove(node.left, node, true, max);
			}
		}
```

```cpp
Node* deleteFromBST(Node* root, int key) {
	if(root == NULL) {
		return NULL;
	}
	if(key < root->data) {
		root->left = deleteFromBST(root->left, key);
	} else if(key > root->data) {
		root->right = deleteFromBST(root->right, key);
	} else {
		if(root->left == NULL and root->right == NULL) {
			delete root;
			return NULL;
		} else if(root->right==NULL) {
			Node *temp = root->left;
			delete root;
			return temp;
		} else if(root->left == NULL) {
			Node *temp = root->right;
			delete root;
			return temp;
		} else {
			Node *right_root = root->right;
			Node *to_be_swap = right_root;
			while(to_be_swap->left != NULL) {
				to_be_swap = to_be_swap->left;
			}
			root->data = to_be_swap->data;
			root->right = deleteFromBST(root->right, root->data);
		}
	}
	return root;
}

```

**Q1- Given a sorted array, construct a possible bst from that (unique bst) (try to make a balanced bst)**

```java
private Node construct(int[] in, int lo, int hi) {

		if (lo > hi) {
			return null;
		}

		// mid element will be root node
		int mid = (lo + hi) / 2;
		// make a new node
		Node nn = new Node();
		nn.data = in[mid];
		

		nn.left = construct(in, lo, mid - 1);
		nn.right = construct(in, mid + 1, hi);

		return nn;
	}
```

**Q2- Check if a given BT is BST**

Assume a BST is defined as follows:

- The left subtree of a node contains only nodes with keys less than the node's key.
- The right subtree of a node contains only nodes with keys greater than the node's key.
- Both the left and right subtrees must also be binary search trees.

_Will this method work????_
-  For each node, check if the left node of it is smaller than the node and right node of it is greater than the node.

Failing in cases like 
![Screenshot 2020-01-17 at 5 10 22 PM](https://user-images.githubusercontent.com/35702912/72610044-67cce380-394c-11ea-9313-e01abfb866b8.png)

_Approach1:_ Write inorder traversal

_Approach2:_ 3 

- Range of the element of the root node: [-inf, +inf]
- Range of the root of left subtree [-inf, root.data)
- Range of the root of left subtree [root.data + 1, inf]


If the current value in any node, is not obeying that range, we can say that the tree is not BST. 

_Approach2:_ 4

Using Custom Object. 

public class Node{
	boolean isBST;
	int min;
	int max;
}
 
**Q3- Find the size of largest Binary Search Tree in BT**

Given a binary tree. Find the size of largest subtree which is a Binary Search Tree (BST), where largest means subtree with the largest number of nodes in it.

Note: A subtree must include all of its descendants.
Three possibilities: 

```java 
class TreeDetail{
public:
	int size;
	bool bst;
	int min;
	int max;

	TreeDetail(){
		size = 0;
		bst = true;
		min = INT_MAX;
		max = INT_MIN;
	}
};

TreeDetail largestBSTinBinaryTree(node*root){
	TreeDetail val;

	if(root==NULL){
		return val;
	}

	TreeDetail leftDetail = largestBSTinBinaryTree(root->left);
	TreeDetail rightDetail = largestBSTinBinaryTree(root->right);

	if(leftDetail.bst == false or rightDetail.bst==false or root->data < leftDetail.max or root->data > rightDetail.min){
		val = new TreeDetail();
		val.bst = false;
		val.size = max(leftDetail.size,rightDetail.size);
		return val;
	}

	val.bst = true;
	val.size = leftDetail.size + rightDetail.size + 1;

	val.min = root->left!=NULL ? leftDetail.min : root->data;

	val.max = root->right!=NULL ? rightDetail.max : root->data;

	return val;
}

```

**Q4- Given a BST, somebody swapped 2 elements, Find out which pair was swapped?**

_Trivial Approach_

- Take inorder of the given tree
- Copy the inorder in a different array and sort it 
- The indexes with different values gives us sorted elements

Intuition - Had it been a perfect bst, both the array would be having same elements in same order, but elements are not in same order, denoting that there is a distortion. 

Time Complexity - O(nlogn)

Space Complexity - O(n)

_Optimised Approach_

We can solve this in O(n) time and with a single traversal of the given BST. Since inorder traversal of BST is always a sorted array, the problem can be reduced to a problem where two elements of a sorted array are swapped. 
There are two cases that we need to handle:

1. The swapped nodes are not adjacent in the inorder traversal of the BST.

 For example, Nodes 5 and 25 are swapped in {3 5 7 8 10 15 20 25}. 
 The inorder traversal of the given tree is 3 25 7 8 10 15 20 5 
If we observe carefully, during inorder traversal, we find node 7 is smaller than the previous visited node 25. Here save the context of node 25 (previous node). Again, we find that node 5 is smaller than the previous node 20. This time, we save the context of node 5 ( current node ). Finally swap the two node’s values.

2. The swapped nodes are adjacent in the inorder traversal of BST.

  For example, Nodes 7 and 8 are swapped in {3 5 7 8 10 15 20 25}. 
  The inorder traversal of the given tree is 3 5 8 7 10 15 20 25 
Unlike case #1, here only one point exists where a node value is smaller than previous node value. e.g. node 7 is smaller than node 8.

How to Solve? We will maintain three pointers, first, middle and last. When we find the first point where current node value is smaller than previous node value, we update the first with the previous node & middle with the current node. When we find the second point where current node value is smaller than previous node value, we update the last with the current node. In case #2, we will never find the second point. So, last pointer will not be updated. After processing, if the last node value is null, then two swapped nodes of BST are adjacent.

```java

void correctBST( Node root ) 
    { 
        // Initialize pointers needed  
        // for correctBSTUtil() 
        first = middle = last = prev = null; 
  
        // Set the poiters to find out  
        // two nodes 
        correctBSTUtil( root ); 
  
        // Fix (or correct) the tree 
        if( first != null && last != null ) 
        { 
            int temp = first.data; 
            first.data = last.data; 
            last.data = temp;  
        } 
        // Adjacent nodes swapped 
        else if( first != null && middle != 
                                    null )  
        { 
            int temp = first.data; 
            first.data = middle.data; 
            middle.data = temp; 
        } 
  
        // else nodes have not been swapped, 
        // passed tree is really BST. 
    } 
    
    void correctBSTUtil( Node root) 
    { 
        if( root != null ) 
        { 
            // Recur for the left subtree 
            correctBSTUtil( root.left); 
  
            // If this node is smaller than 
            // the previous node, it's  
            // violating the BST rule. 
?

```

**Q5- Given a BST, Given the root and another pointer to another node, What is the next element in the inorder traversal after this pointer's node?**
**Inorder Successor of BST**

1) If right subtree of node is not NULL, then succ lies in right subtree. Do following.
Go to right subtree and return the node with minimum key value in right subtree.
2) If right sbtree of node is NULL, then start from root and us search like technique. Do following.


```cpp

struct node * inOrderSuccessor(struct node *root, struct node *n) 
{ 
    // step 1 of the above algorithm 
    if( n->right != NULL ) 
        return minValue(n->right); 
  
    struct node *succ = NULL; 
  
    // Start from root and search for successor down the tree 
    while (root != NULL) 
    { 
        if (n->data < root->data) 
        { 
            succ = root; 
            root = root->left; 
        } 
        else if (n->data > root->data) 
            root = root->right; 
        else
           break; 
    } 
  
    return succ; 
} 
```

```java
public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {

        TreeNode candidate = null;
        TreeNode cur = root;

        while (cur != null) {
            if (cur.val > p.val) {
                candidate = cur;
                cur = cur.left;
            } else {
                // cur.val <= p.val
                cur = cur.right;
            }
        }

        return candidate;
    }
```

Time Complexity: O(n)
Space Complexity: O(n)

## Extra Problem

**Q- Given a complete binary tree with N nodes and each node have an distinct integer ai attached with it, find the minimum number of swaps you can make to convert the binary tree into binary search tree. In one swap, you can select any two nodes and swap their values.
You will be given the array representation of the binary tree. Root of the tree will be at a<sub>1</sub>. Left child of root will be at a<sub>2</sub> and right child of root will be at a<sub>3</sub>. Left child of node at array position k will be at a<sub>2k</sub> and right child of node at array position k will be at a<sub>2k+1</sub>.**

https://www.hackerearth.com/practice/data-structures/trees/binary-search-tree/practice-problems/algorithm/little-monk-and-swaps/editorial/



