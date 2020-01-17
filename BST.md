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

**Q1- Print in Range**

Print all the keys of tree in range k1 to k2. i.e. print all x such that k1<=x<=k2 and x is a key of given BST. Print all the keys in increasing order.

```java
public void printInRange(int lower, int upper) {

		printInRange(this.root, lower, upper);

	}
	private void printInRange(Node node, int lower, int upper) {
		if (node == null) {
			return;
		}
		if (node.data > upper) {
			printInRange(node.left, lower, upper);
		}
		else if (node.data < lower) {
			printInRange(node.right, lower, upper);
		}
		else {
			printInRange(node.left, lower, upper);
			System.out.println(node.data);
			printInRange(node.right, lower, upper);
		}
	}
```
**Q2- Check if a given BT is BST**

_Will this method work????_
-  For each node, check if the left node of it is smaller than the node and right node of it is greater than the node.

Failing in cases like 
![Screenshot 2020-01-17 at 5 10 22 PM](https://user-images.githubusercontent.com/35702912/72610044-67cce380-394c-11ea-9313-e01abfb866b8.png)

_Approach1:_ Write inorder traversal

_Approach2:_ 3 conditions:
- left subtree is a BST
- right subtree is a BST
- root is greater than the max value in left subtree
- root is less than the lowest value in right subtree

```java
	public class Mover {
		boolean isbst;
	}

	private Mover IsBST(Node node) {

		if (node == null) {
			Mover m = new Mover();
			m.isbst = true;
			return m;
		}

		Mover l = IsBST(node.left);
		Mover r = IsBST(node.right);

		Mover ans = new Mover();
		if (node.left != null && node.right != null) {
			if (node.left.data < node.data && node.right.data > node.data && l.isbst && r.isbst) {
				ans.isbst = true;
			} else {
				ans.isbst = false;
			}
		}

		if (node.left != null && node.right == null) {
			if (node.left.data < node.data && l.isbst && r.isbst) {
				ans.isbst = true;
			} else {
				ans.isbst = false;
			}
		}

		if (node.left == null && node.right == null) {
			if (l.isbst && r.isbst) {
				ans.isbst = true;
			} else {
				ans.isbst = false;
			}
		}

		if (node.left == null && node.right != null) {
			if (node.right.data > node.data && l.isbst && r.isbst) {
				ans.isbst = true;
			} else {
				ans.isbst = false;
			}
		}

		return ans;
	}
```

**Q3- Find the size of largest Binary Search Tree in BT**

Three possibilities: 
```cpp
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
            if (prev != null && root.data < 
                                prev.data) 
            { 
                // If this is first violation, 
                // mark these two nodes as 
                // 'first' and 'middle' 
                if (first == null) 
                { 
                    first = prev; 
                    middle = root; 
                } 
  
                // If this is second violation, 
                // mark this node as last 
                else
                    last = root; 
            } 
  
            // Mark this node as previous 
            prev = root; 
  
            // Recur for the right subtree 
            correctBSTUtil( root.right); 
        } 
    } 

```
Time Complexity - O(n)
Space Complexity - O(n)

**Q5- Build BST from unsorted array**
Keep on adding elements by traversing the array.

```java
//insert
Node insert(node, value) {
    if node is null
        // Create a leaf.
        // It might be the root...
        return new Node(value)

    // It's occupied, see which way to
    // go based on it's value

    // right? ...
    if value > node.value
        node.right = insert(node.right, value)

    // or left?
    else if value < node.value
        node.left = insert(node.left, value)

    // Code is not handling dups.
    return node
}

//construct

Node arrayToBinary(array, root){
    for e in array
        root = insert(root, e)
    return root
}

```
**Q6- Given a BST, Given the root and another pointer to another node, What is the next element in the inorder traversal after this pointer's node?**

- Case 1: What if there is a right subtree of the given node? -> Get the leftmost of the right subtree of the given node
- Case 2: What if there is no right subtree?


**Q7- Given a sorted array, construct a possible bst from that (unique bst) (try to make a balanced bst)**

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

**Q8- Increasing Order Search Tree: Given a binary search tree, rearrange the tree in in-order so that the leftmost node in the tree is now the root of the tree, and every node has no left child and only 1 right child.**

```cpp
class Custom {
public:
    TreeNode *head;
    TreeNode *tail;
    Custom(TreeNode *head, TreeNode *tail) {
        this->head = head;
        this->tail = tail;
    }
};

class Solution {
public:
    Custom *helper(TreeNode* root) {
        if(root == NULL) return NULL;
        Custom* lf = helper(root->left);
        if(lf!=NULL) {
            root->left = NULL;
            lf->tail->right = root;
        } 
        Custom* rh = helper(root->right);
        if(rh!=NULL) {
            root->right = rh->head;
        }
        return new Custom((lf!=NULL)?lf->head:root, (rh!=NULL)?rh->tail:root);
    }
    
    
    TreeNode* increasingBST(TreeNode* root) {
        Custom* c = helper(root);
        return c->head;
    }
};
```

```java

```

**Q (Optional)- Convert a BST into min heap with a constraint that all values in left. Subtree are less than the values in right subtree**

Given a binary search tree which is also a complete binary tree. The problem is to convert the given BST into a Min Heap with the condition that all the values in the left subtree of a node should be less than all the values in the right subtree of the node. This condition is applied on all the nodes in the so converted Min Heap.

![Screenshot 2020-01-17 at 5 48 04 PM](https://user-images.githubusercontent.com/35702912/72612030-9bf6d300-3951-11ea-8039-5e659a115a69.png)

_Min Heap_

All the nodes in the Min Heap satisfies the given condition, that is, values in the left subtree of a node should be less than the values in the right subtree of the node. 

**Homwwork Problem*

**Q- Given a complete binary tree with N nodes and each node have an distinct integer ai attached with it, find the minimum number of swaps you can make to convert the binary tree into binary search tree. In one swap, you can select any two nodes and swap their values.
You will be given the array representation of the binary tree. Root of the tree will be at a<sub>1</sub>. Left child of root will be at a<sub>2</sub> and right child of root will be at a<sub>3</sub>. Left child of node at array position k will be at a<sub>2k</sub> and right child of node at array position k will be at a<sub>2k+1</sub>.**

https://www.hackerearth.com/practice/data-structures/trees/binary-search-tree/practice-problems/algorithm/little-monk-and-swaps/editorial/
